# Implementation Plan: Option Picker for Run Page

## Overview

Add an "Add Options..." button to the Run page that opens a dialog letting users browse all `--help` options, select them, and assign them to either the Main Settings group or an Advanced group. Added options persist across sessions, render as `OptionCard` editors, and can be removed.

---

## Critical Design Issues Found

### Issue 1: Value persistence vs UI layout persistence

The original plan proposed storing everything in `user_options.json`. This conflates two concerns:

- **UI layout** (which options are visible, where they go) → should persist across sessions
- **Option values** (what the user sets `--mirostat` to) → should flow through existing profile/config mechanisms

**Resolution:** `user_options.json` stores only UI layout (flag + destination). Option values are stored by the existing mechanism:
- `profile.raw_args` for per-profile values (via `_settings_from_form()`)
- `config.global_settings` for global defaults

This means user-added options integrate seamlessly with the existing save/load/profile-switch flow.

### Issue 2: `_schema_options_by_id` must include user-added options

`_load_profile_into_form()` (run.py:1415) iterates `self._editors` and calls `_load_unknown_editor()` for non-catalog options. But `_load_unknown_editor()` looks up `self._schema_options_by_id[option_id]` to get the `RuntimeOption` (flag, kind, default).

If user-added options aren't in `_schema_options_by_id`, profile loading will silently skip them — their editors won't be populated from `raw_args`.

**Resolution:** After creating user-added option editors, register their `RuntimeOption` in `self._schema_options_by_id`.

### Issue 3: VersionedEnvelope pattern

All existing stores use `VersionedEnvelope` + migration chains (see `stores.py`). The new `UserOptionStore` should follow the same pattern for consistency and future-proofing.

### Issue 4: Main settings grid layout

`_build_main_settings()` (run.py:412) uses a fixed 2-column grid with first 16 `MAIN_OPTION_IDS`, then a horizontal row for items 16+. Injecting user options into this grid would require dynamic row/column recalculation.

**Resolution:** Add a separate "User Options" sub-section below the existing grid (inside the same Card). This keeps the curated layout intact and gives user options their own visual area.

### Issue 5: Group destination naming

The plan proposed storing group slugs (`"sampling"`), but the codebase has an inconsistent mapping:
- Parser slugs: `"model_loading"`, `"performance"`, `"server_api"`, `"sampling"`, etc.
- Catalog display names: `"Model loading"`, `"Performance"`, `"Server / API"`, `"Sampling"`, etc.
- `_GROUP_DISPLAY` (run.py:60-84) maps both formats to display names

**Resolution:** Store the catalog display name format (e.g., `"Sampling"`, `"Context / KV cache"`) since that's what `_GROUP_DISPLAY` expects and what `_build_schema_advanced` uses as tab labels. Use `_GROUP_DISPLAY` to normalize when looking up.

### Issue 6: Missing destination group tab

If a user assigns an option to a group that has no other options (e.g., "General / Miscellaneous"), that tab won't exist yet.

**Resolution:** `_build_schema_advanced()` must create the destination tab if it doesn't exist, or inject user options after the main loop by checking which tabs exist.

### Issue 7: Editor state across rebuilds

When "Add Selected" triggers a full rebuild (`_build_main_settings` + `_build_advanced_groups`), all editors are destroyed and recreated. This is fine because `_load_profile_into_form()` is called after `build()` and restores values from the profile.

But there's a timing issue: `build()` calls `_build_main_settings()` → `_build_advanced_groups()` → then `_load_profile_into_form()` is NOT called during build. It's only called when the profile combo changes. So after a rebuild, editors may show defaults instead of current values.

**Resolution:** After rebuilding (triggered by "Add Selected"), explicitly call `_load_profile_into_form()` to restore editor values. Or better: capture current editor values before rebuild, then restore after.

### Issue 8: `_load_unknown_editor` only handles schema options

`_load_unknown_editor()` (run.py:1114) assumes the option exists in `self._schema_options_by_id`. For user-added options that are registered there (per Issue 2), this works. But we need to verify the method handles the case where a user-added option's flag is found in `raw_args` but the option was just added (no prior value).

**Resolution:** This works naturally — if the flag isn't in `raw_args`, the editor stays at its default. If it is, the value is restored.

---

## Revised Implementation Plan

### Phase 1: Data Model & Persistence

#### 1.1 Add to `qt_app/llama_data/paths.py`

Add `USER_OPTIONS_FILE = "user_options.json"` constant.

Add `user_options_path: Path` to `DataPaths` dataclass.

Update `default_paths()` to include it.

#### 1.2 Add to `qt_app/llama_data/models.py`

```python
@dataclass
class UserOptionEntry:
    flag: str           # canonical flag, e.g. "--mirostat"
    destination: str    # "main" or group display name, e.g. "Sampling"

@dataclass
class UserOptions:
    version: int = 1
    options: list[UserOptionEntry] = field(default_factory=list)

    def to_json(self) -> dict[str, Any]: ...
    @classmethod
    def from_json(cls, data: Any) -> "UserOptions": ...
```

#### 1.3 Add `UserOptionStore` to `qt_app/llama_data/stores.py`

Follow the existing pattern:
- Migration chain: `USER_OPTIONS_MIGRATIONS: dict[int, Migration]`
- Write lock: `_USER_OPTIONS_WRITE_LOCK = threading.RLock()`
- `load()` → `UserOptions`
- `save(options: UserOptions)` → writes via `VersionedEnvelope`

#### 1.4 Wire into `qt_app/app/main_window.py`

- Load `UserOptionStore` alongside other stores
- Pass to `RunPage` constructor

---

### Phase 2: Option Picker Dialog

#### 2.1 Create dialog class in `qt_app/app/pages/run.py` (or separate file if >200 lines)

```python
class OptionPickerDialog(QDialog):
    option_added = Signal()  # emitted after options are added
```

**Layout:**
- Search box at top (filters by flag name and description)
- Collapsible sections per group (reusing `CollapsibleGroup` widget)
- Each option row: `QCheckBox` + flag (mono font) + description (elided)
- Only shows options NOT already in `MAIN_OPTION_IDS` and NOT already user-added
- Destination dropdown: "Main Settings" + all group display names from `_GROUP_DISPLAY`
- Default destination = option's parsed group (mapped through `_GROUP_DISPLAY`)
- "Add Selected (N)" button with count, disabled if N=0
- On accept: writes to `UserOptionStore`, triggers rebuild

#### 2.2 Data source

Reads from `self._schema.options` (the parsed `--help` output). If `self._schema` is None, shows message: "Configure a llama-server binary in Settings to browse available options."

---

### Phase 3: Rendering User-Added Options

#### 3.1 Add "Add Options..." button to Advanced Groups header

In `_build_advanced_groups()` (run.py:478), add a `SecondaryButton("Add Options…")` to the `header_layout` (next to the toggle button, search box, and filter pill).

#### 3.2 Inject into Main Settings

In `_build_main_settings()` (run.py:412), after the existing grid and raw extras:

```python
# User-added options for Main Settings
user_opts = self._user_option_store.load()
main_user_opts = [e for e in user_opts.options if e.destination == "main"]
if main_user_opts:
    heading = QLabel("User options", card)
    heading.setObjectName("CardTitle")
    layout.addWidget(heading)
    user_grid = QGridLayout()
    # ... create OptionCard + editor for each, with × removal button
```

#### 3.3 Inject into Advanced Groups

In `_build_schema_advanced()` (run.py:629), after building each group's tab, check for user-added options assigned to that group and append them to the tab's grid.

If a user option's destination group doesn't have a tab yet, create one.

#### 3.4 Register in `_schema_options_by_id`

After creating each user-added option's editor:

```python
# Ensure the RuntimeOption is available for profile loading
if rt_opt.id not in self._schema_options_by_id:
    self._schema_options_by_id[rt_opt.id] = rt_opt
```

This ensures `_load_profile_into_form()` → `_load_unknown_editor()` can find the option metadata.

#### 3.5 Removal mechanism

Each user-added `OptionCard` gets a `QPushButton("×")` styled as a subtle close button.

On click:
1. Remove from `UserOptionStore`
2. Remove the `OptionCard` widget from the layout
3. Remove the editor from `self._editors`
4. Remove from `self._schema_options_by_id` if it was user-added
5. No full rebuild needed — surgical removal

---

### Phase 4: Rebuild & Value Restoration

#### 4.1 After adding options (from dialog)

1. Save to `UserOptionStore`
2. Capture current form values: `settings, raw_args, user_set = self._settings_from_form()`
3. Rebuild: `_build_main_settings()` + `_build_advanced_groups()`
4. Restore values: create a temporary `ModelProfile` from captured values and call `_load_profile_into_form()` equivalent
5. Update command preview

#### 4.2 After removing options

Surgical removal (Phase 3.5) — no rebuild needed.

---

### Phase 5: Integration with Existing Flows

#### 5.1 `_settings_from_form()` (run.py:1243)

No changes needed. Already iterates `self._editors` and handles both curated and unknown options. User-added options flow into `raw_args` naturally.

#### 5.2 `_load_profile_into_form()` (run.py:1415)

No changes needed IF user-added options are registered in `_schema_options_by_id` (Phase 3.4). The existing `_load_unknown_editor()` call handles them.

#### 5.3 `build_argv()` (runtime.py:251)

No changes needed. User-added option values arrive via `profile.raw_args` (from `_settings_from_form()` → `_save_profile()` → `build_argv()`).

#### 5.4 `_argv()` (run.py:1634)

No changes needed. Already calls `_settings_from_form()` which collects user-added option values.

---

### Phase 6: Edge Cases

#### 6.1 Binary not configured
Dialog shows: "Configure a llama-server binary in Settings to browse available options."

#### 6.2 Option not supported by current binary
Still render the OptionCard but with a warning chip/tooltip: "Not supported by current binary."

#### 6.3 Binary changes
User-added options re-checked against new schema. Unsupported ones shown as disabled.

#### 6.4 User options file missing/corrupt
Fall back to empty `UserOptions()`. Log warning.

#### 6.5 Group destination tab doesn't exist
Create the tab dynamically when injecting user options.

#### 6.6 Duplicate prevention
Picker filters out options already in `MAIN_OPTION_IDS` and already user-added.

---

## Files to Modify

| File | Changes |
|------|---------|
| `qt_app/llama_data/paths.py` | Add `USER_OPTIONS_FILE`, `user_options_path` to `DataPaths` |
| `qt_app/llama_data/models.py` | Add `UserOptionEntry`, `UserOptions` dataclasses |
| `qt_app/llama_data/stores.py` | Add `UserOptionStore` class |
| `qt_app/app/main_window.py` | Load `UserOptionStore`, pass to `RunPage` |
| `qt_app/app/pages/run.py` | Add `OptionPickerDialog`, modify `_build_main_settings()`, `_build_schema_advanced()`, add "Add Options…" button, add removal logic, register user options in `_schema_options_by_id` |

## Implementation Order

1. **Paths + Models + Store** — data layer (isolated, testable)
2. **MainWindow wiring** — pass store to RunPage
3. **OptionPickerDialog** — self-contained dialog
4. **"Add Options…" button** — wire dialog to RunPage header
5. **Main Settings injection** — render user options in main section
6. **Advanced Groups injection** — render user options in tabs
7. **`_schema_options_by_id` registration** — ensure profile loading works
8. **Removal mechanism** — × button on each added OptionCard
9. **Value restoration after rebuild** — capture/restore form values
10. **Edge cases** — unsupported options, missing schema, binary changes

---

## What Changed from v1 Plan

1. **Values vs layout separation**: `user_options.json` stores only UI layout; values flow through existing `raw_args` mechanism
2. **`_schema_options_by_id` registration**: New step to ensure profile loading works
3. **VersionedEnvelope**: Store follows existing pattern
4. **Main settings sub-section**: Separate area rather than mixing into existing grid
5. **Group naming**: Store display names, not slugs (matches `_GROUP_DISPLAY`)
6. **Value restoration**: Explicit capture/restore around rebuild
7. **No changes to `build_argv` or `_settings_from_form`**: They already handle unknown options
