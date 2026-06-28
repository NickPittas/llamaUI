# Missing llama-server Options Catalog

Options from `llama-server --help` not currently in the curated UI catalog.
Select options by number to add to the program.

---

## 1. `--samplers`
**Group:** Sampling
**Description:** Samplers used for generation in order, separated by `;`
**Control:** text input
**Values:** free text (semicolon-separated sampler names)
**Default:** `penalties;dry;top_n_sigma;top_k;typ_p;top_p;min_p;xtc;temperature`

## 2. `--repeat-last-n`
**Group:** Sampling
**Description:** Last n tokens to consider for penalize
**Control:** spinbox (int)
**Values:** 0 to context size, 0=disabled, -1=context size
**Default:** 64

## 3. `--presence-penalty`
**Group:** Sampling
**Description:** Repeat alpha presence penalty
**Control:** slider (float)
**Values:** 0.0 to 2.0
**Default:** 0.00

## 4. `--frequency-penalty`
**Group:** Sampling
**Description:** Repeat alpha frequency penalty
**Control:** slider (float)
**Values:** 0.0 to 2.0
**Default:** 0.00

## 5. `--dry-multiplier`
**Group:** Sampling
**Description:** DRY sampling multiplier
**Control:** slider (float)
**Values:** 0.0 to 5.0, 0.0=disabled
**Default:** 0.00

## 6. `--dry-base`
**Group:** Sampling
**Description:** DRY sampling base value
**Control:** slider (float)
**Values:** 1.0 to 10.0
**Default:** 1.75

## 7. `--dry-allowed-length`
**Group:** Sampling
**Description:** Allowed length for DRY sampling
**Control:** spinbox (int)
**Values:** 1 to 100
**Default:** 2

## 8. `--dry-penalty-last-n`
**Group:** Sampling
**Description:** DRY penalty for last n tokens
**Control:** spinbox (int)
**Values:** -1 to context size, 0=disable, -1=context size
**Default:** -1

## 9. `--dry-sequence-breaker`
**Group:** Sampling
**Description:** Sequence breaker for DRY sampling
**Control:** text input
**Values:** free text (characters), "none" to disable
**Default:** `\n`, `:`, `"`, `*`

## 10. `--adaptive-target`
**Group:** Sampling
**Description:** Adaptive-p: select tokens near this probability
**Control:** slider (float)
**Values:** -1.0 to 1.0, negative=disabled
**Default:** -1.00

## 11. `--adaptive-decay`
**Group:** Sampling
**Description:** Adaptive-p: decay rate for target adaptation over time
**Control:** slider (float)
**Values:** 0.0 to 0.99
**Default:** 0.90

## 12. `--dynatemp-range`
**Group:** Sampling
**Description:** Dynamic temperature range
**Control:** slider (float)
**Values:** 0.0 to 5.0, 0.0=disabled
**Default:** 0.00

## 13. `--dynatemp-exp`
**Group:** Sampling
**Description:** Dynamic temperature exponent
**Control:** slider (float)
**Values:** 0.0 to 10.0
**Default:** 1.00

## 14. `--mirostat`
**Group:** Sampling
**Description:** Mirostat sampling mode
**Control:** dropdown
**Values:** 0=disabled, 1=Mirostat, 2=Mirostat 2.0
**Default:** 0

## 15. `--mirostat-lr`
**Group:** Sampling
**Description:** Mirostat learning rate (eta)
**Control:** slider (float)
**Values:** 0.0 to 1.0
**Default:** 0.10

## 16. `--mirostat-ent`
**Group:** Sampling
**Description:** Mirostat target entropy (tau)
**Control:** slider (float)
**Values:** 0.0 to 20.0
**Default:** 5.00

## 17. `--xtc-probability`
**Group:** Sampling
**Description:** XTC probability
**Control:** slider (float)
**Values:** 0.0 to 1.0, 0.0=disabled
**Default:** 0.00

## 18. `--xtc-threshold`
**Group:** Sampling
**Description:** XTC threshold
**Control:** slider (float)
**Values:** 0.0 to 1.0, 1.0=disabled
**Default:** 0.10

## 19. `--top-n-sigma`
**Group:** Sampling
**Description:** Top-n-sigma sampling
**Control:** slider (float)
**Values:** -1.0 to 5.0, -1.0=disabled
**Default:** -1.00

## 20. `--typical-p`
**Group:** Sampling
**Description:** Locally typical sampling (p)
**Control:** slider (float)
**Values:** 0.0 to 1.0, 1.0=disabled
**Default:** 1.00

## 21. `--ignore-eos`
**Group:** Sampling
**Description:** Ignore end-of-stream token, continue generating
**Control:** checkbox
**Values:** on/off
**Default:** off

## 22. `--logit-bias`
**Group:** Sampling
**Description:** Modify likelihood of specific tokens
**Control:** text input
**Values:** TOKEN_ID(+/-)BIAS, comma-separated
**Default:** (none)

## 23. `--grammar`
**Group:** Sampling
**Description:** BNF-like grammar to constrain generations
**Control:** text input
**Values:** free text (BNF grammar)
**Default:** (none)

## 24. `--grammar-file`
**Group:** Sampling
**Description:** File to read grammar from
**Control:** file picker
**Values:** file path
**Default:** (none)

## 25. `--json-schema`
**Group:** Sampling
**Description:** JSON schema to constrain generations
**Control:** text input
**Values:** free text (JSON)
**Default:** (none)

## 26. `--json-schema-file`
**Group:** Sampling
**Description:** File containing JSON schema
**Control:** file picker
**Values:** file path
**Default:** (none)

## 27. `--backend-sampling`
**Group:** Sampling
**Description:** Enable backend sampling (experimental)
**Control:** checkbox
**Values:** on/off
**Default:** off

## 28. `--keep`
**Group:** Context / KV cache
**Description:** Tokens to keep from initial prompt
**Control:** spinbox (int)
**Values:** -1 to context size, -1=all
**Default:** 0

## 29. `--swa-full`
**Group:** Context / KV cache
**Description:** Use full-size SWA cache
**Control:** checkbox
**Values:** on/off
**Default:** off

## 30. `--rope-scale`
**Group:** Context / KV cache
**Description:** RoPE context scaling factor
**Control:** slider (float)
**Values:** 0.0 to 100.0
**Default:** (from model)

## 31. `--yarn-orig-ctx`
**Group:** Context / KV cache
**Description:** YaRN: original context size of model
**Control:** spinbox (int)
**Values:** 0 to 1000000, 0=model training context
**Default:** 0

## 32. `--yarn-ext-factor`
**Group:** Context / KV cache
**Description:** YaRN: extrapolation mix factor
**Control:** slider (float)
**Values:** -1.0 to 10.0, 0.0=full interpolation
**Default:** -1.00

## 33. `--yarn-attn-factor`
**Group:** Context / KV cache
**Description:** YaRN: attention magnitude scale
**Control:** slider (float)
**Values:** -1.0 to 10.0
**Default:** -1.00

## 34. `--yarn-beta-slow`
**Group:** Context / KV cache
**Description:** YaRN: high correction dim (alpha)
**Control:** slider (float)
**Values:** -1.0 to 10.0
**Default:** -1.00

## 35. `--yarn-beta-fast`
**Group:** Context / KV cache
**Description:** YaRN: low correction dim (beta)
**Control:** slider (float)
**Values:** -1.0 to 10.0
**Default:** -1.00

## 36. `--kv-unified`
**Group:** Context / KV cache
**Description:** Use single unified KV buffer shared across all sequences
**Control:** checkbox
**Values:** on/off
**Default:** on (if slots=auto)

## 37. `--cache-ram`
**Group:** Context / KV cache
**Description:** Max cache size in MiB
**Control:** spinbox (int)
**Values:** -1 to 65536, -1=no limit, 0=disable
**Default:** 8192

## 38. `--cache-reuse`
**Group:** Context / KV cache
**Description:** Min chunk size to reuse from cache via KV shifting
**Control:** spinbox (int)
**Values:** 0 to 65536
**Default:** 0

## 39. `--cache-idle-slots`
**Group:** Context / KV cache
**Description:** Save idle slots to prompt cache on new task
**Control:** checkbox
**Values:** on/off
**Default:** on

## 40. `--ctx-checkpoints`
**Group:** Context / KV cache
**Description:** Max context checkpoints per slot
**Control:** spinbox (int)
**Values:** 0 to 256
**Default:** 32

## 41. `--checkpoint-min-step`
**Group:** Context / KV cache
**Description:** Minimum spacing between context checkpoints (tokens)
**Control:** spinbox (int)
**Values:** 0 to 65536
**Default:** 256

## 42. `--context-shift`
**Group:** Context / KV cache
**Description:** Use context shift on infinite text generation
**Control:** checkbox
**Values:** on/off
**Default:** off

## 43. `--device`
**Group:** GPU / offload
**Description:** Comma-separated devices for offloading
**Control:** text input
**Values:** device names, comma-separated
**Default:** (none)

## 44. `--fit`
**Group:** GPU / offload
**Description:** Adjust unset args to fit in device memory
**Control:** dropdown
**Values:** on, off
**Default:** on

## 45. `--fit-target`
**Group:** GPU / offload
**Description:** Target margin per device for --fit (MiB)
**Control:** text input
**Values:** comma-separated MiB values
**Default:** 1024

## 46. `--fit-ctx`
**Group:** GPU / offload
**Description:** Minimum ctx size for --fit option
**Control:** spinbox (int)
**Values:** 256 to 1048576
**Default:** 4096

## 47. `--op-offload`
**Group:** GPU / offload
**Description:** Offload host tensor operations to device
**Control:** checkbox
**Values:** on/off
**Default:** on

## 48. `--cpu-moe`
**Group:** GPU / offload
**Description:** Keep all MoE weights in CPU
**Control:** checkbox
**Values:** on/off
**Default:** off

## 49. `--n-cpu-moe`
**Group:** GPU / offload
**Description:** Keep MoE weights of first N layers in CPU
**Control:** spinbox (int)
**Values:** 0 to 999
**Default:** 0

## 50. `--override-tensor`
**Group:** GPU / offload
**Description:** Override tensor buffer type
**Control:** text input
**Values:** tensor_pattern=buffer_type,...
**Default:** (none)

## 51. `--repack`
**Group:** GPU / offload
**Description:** Enable weight repacking
**Control:** checkbox
**Values:** on/off
**Default:** on

## 52. `--check-tensors`
**Group:** GPU / offload
**Description:** Check model tensor data for invalid values
**Control:** checkbox
**Values:** on/off
**Default:** off

## 53. `--threads-batch`
**Group:** Performance
**Description:** Threads for batch/prompt processing
**Control:** spinbox (int)
**Values:** 0 to 256
**Default:** same as --threads

## 54. `--cpu-mask`
**Group:** Performance
**Description:** CPU affinity mask (hex)
**Control:** text input
**Values:** hex string
**Default:** ""

## 55. `--cpu-range`
**Group:** Performance
**Description:** Range of CPUs for affinity
**Control:** text input
**Values:** lo-hi
**Default:** (none)

## 56. `--cpu-strict`
**Group:** Performance
**Description:** Use strict CPU placement
**Control:** dropdown
**Values:** 0, 1
**Default:** 0

## 57. `--prio`
**Group:** Performance
**Description:** Process/thread priority
**Control:** dropdown
**Values:** -1=low, 0=normal, 1=medium, 2=high, 3=realtime
**Default:** 0

## 58. `--poll`
**Group:** Performance
**Description:** Polling level to wait for work
**Control:** slider (int)
**Values:** 0 to 100
**Default:** 50

## 59. `--numa`
**Group:** Performance
**Description:** NUMA optimizations
**Control:** dropdown
**Values:** distribute, isolate, numactl
**Default:** (none)

## 60. `--threads-http`
**Group:** Performance
**Description:** Threads for HTTP requests
**Control:** spinbox (int)
**Values:** -1 to 256
**Default:** -1

## 61. `--direct-io`
**Group:** Performance
**Description:** Use DirectIO if available
**Control:** checkbox
**Values:** on/off
**Default:** off

## 62. `--lora`
**Group:** Model loading
**Description:** Path to LoRA adapter(s)
**Control:** file picker (multi)
**Values:** comma-separated file paths
**Default:** (none)

## 63. `--lora-scaled`
**Group:** Model loading
**Description:** LoRA adapter with user-defined scaling
**Control:** text input
**Values:** FNAME:SCALE,...
**Default:** (none)

## 64. `--lora-init-without-apply`
**Group:** Model loading
**Description:** Load LoRA without applying (apply via API later)
**Control:** checkbox
**Values:** on/off
**Default:** off

## 65. `--control-vector`
**Group:** Model loading
**Description:** Add a control vector
**Control:** file picker
**Values:** file path
**Default:** (none)

## 66. `--control-vector-scaled`
**Group:** Model loading
**Description:** Control vector with scaling
**Control:** text input
**Values:** FNAME:SCALE,...
**Default:** (none)

## 67. `--control-vector-layer-range`
**Group:** Model loading
**Description:** Layer range for control vectors
**Control:** text input
**Values:** START END
**Default:** (none)

## 68. `--hf-repo`
**Group:** Model loading
**Description:** Hugging Face model repository
**Control:** text input
**Values:** user/model[:quant]
**Default:** (none)

## 69. `--hf-file`
**Group:** Model loading
**Description:** Hugging Face model file override
**Control:** text input
**Values:** filename
**Default:** (none)

## 70. `--model-url`
**Group:** Model loading
**Description:** Model download URL
**Control:** text input
**Values:** URL
**Default:** (none)

## 71. `--docker-repo`
**Group:** Model loading
**Description:** Docker Hub model repository
**Control:** text input
**Values:** [repo/]model[:quant]
**Default:** (none)

## 72. `--override-kv`
**Group:** Model loading
**Description:** Override model metadata by key
**Control:** text input
**Values:** KEY=TYPE:VALUE,...
**Default:** (none)

## 73. `--mmproj-url`
**Group:** Multimodal
**Description:** URL to multimodal projector file
**Control:** text input
**Values:** URL
**Default:** (none)

## 74. `--mmproj-auto`
**Group:** Multimodal
**Description:** Auto-use mmproj if available
**Control:** checkbox
**Values:** on/off
**Default:** on

## 75. `--mmproj-offload`
**Group:** Multimodal
**Description:** GPU offloading for multimodal projector
**Control:** checkbox
**Values:** on/off
**Default:** on

## 76. `--image-min-tokens`
**Group:** Multimodal
**Description:** Min tokens per image (dynamic resolution)
**Control:** spinbox (int)
**Values:** 0 to 65536
**Default:** (from model)

## 77. `--image-max-tokens`
**Group:** Multimodal
**Description:** Max tokens per image (dynamic resolution)
**Control:** spinbox (int)
**Values:** 0 to 65536
**Default:** (from model)

## 78. `--mtmd-batch-max-tokens`
**Group:** Multimodal
**Description:** Max image tokens per batch
**Control:** spinbox (int)
**Values:** 1 to 65536
**Default:** 1024

## 79. `--api-key-file`
**Group:** Server / API
**Description:** Path to file containing API keys
**Control:** file picker
**Values:** file path
**Default:** (none)

## 80. `--api-prefix`
**Group:** Server / API
**Description:** Prefix path for server API
**Control:** text input
**Values:** string
**Default:** ""

## 81. `--ssl-key-file`
**Group:** Server / API
**Description:** SSL private key file
**Control:** file picker
**Values:** file path
**Default:** (none)

## 82. `--ssl-cert-file`
**Group:** Server / API
**Description:** SSL certificate file
**Control:** file picker
**Values:** file path
**Default:** (none)

## 83. `--path`
**Group:** Server / API
**Description:** Path to serve static files from
**Control:** text input
**Values:** directory path
**Default:** ""

## 84. `--reuse-port`
**Group:** Server / API
**Description:** Allow multiple sockets on same port
**Control:** checkbox
**Values:** on/off
**Default:** off

## 85. `--timeout`
**Group:** Server / API
**Description:** Server read/write timeout in seconds
**Control:** spinbox (int)
**Values:** 1 to 86400
**Default:** 3600

## 86. `--sse-ping-interval`
**Group:** Server / API
**Description:** SSE ping interval in seconds
**Control:** spinbox (int)
**Values:** -1 to 300, -1=disabled
**Default:** 30

## 87. `--slot-prompt-similarity`
**Group:** Server / API
**Description:** Prompt match threshold to reuse a slot
**Control:** slider (float)
**Values:** 0.0 to 1.0, 0.0=disabled
**Default:** 0.10

## 88. `--slot-save-path`
**Group:** Server / API
**Description:** Path to save slot KV cache
**Control:** text input
**Values:** directory path
**Default:** (disabled)

## 89. `--media-path`
**Group:** Server / API
**Description:** Directory for loading local media files
**Control:** text input
**Values:** directory path
**Default:** (disabled)

## 90. `--props`
**Group:** Server / API
**Description:** Enable POST /props endpoint
**Control:** checkbox
**Values:** on/off
**Default:** off

## 91. `--embedding`
**Group:** Server / API
**Description:** Restrict to embedding use case only
**Control:** checkbox
**Values:** on/off
**Default:** off

## 92. `--rerank`
**Group:** Server / API
**Description:** Enable reranking endpoint
**Control:** checkbox
**Values:** on/off
**Default:** off

## 93. `--tools`
**Group:** Server / API
**Description:** Enable built-in tools for AI agents
**Control:** text input
**Values:** "all" or comma-separated tool names
**Default:** (none)

## 94. `--agent`
**Group:** Server / API
**Description:** Enable CORS proxy + all built-in tools
**Control:** checkbox
**Values:** on/off
**Default:** off

## 95. `--ui`
**Group:** Server / API
**Description:** Enable/disable the Web UI
**Control:** checkbox
**Values:** on/off
**Default:** on

## 96. `--cache-prompt`
**Group:** Server / API
**Description:** Enable prompt caching
**Control:** checkbox
**Values:** on/off
**Default:** on

## 97. `--models-dir`
**Group:** Server / API
**Description:** Directory for router server models
**Control:** text input
**Values:** directory path
**Default:** (disabled)

## 98. `--models-preset`
**Group:** Server / API
**Description:** Path to INI file with model presets
**Control:** file picker
**Values:** file path
**Default:** (disabled)

## 99. `--models-autoload`
**Group:** Server / API
**Description:** Auto-load models in router mode
**Control:** checkbox
**Values:** on/off
**Default:** on

## 100. `--chat-template`
**Group:** Chat / Template
**Description:** Set custom Jinja chat template
**Control:** dropdown
**Values:** bailing, bailing-think, bailing2, chatglm3, chatglm4, chatml, command-r, deepseek, deepseek-ocr, deepseek2, deepseek3, exaone-moe, exaone3, exaone4, falcon3, gemma, gigachat, glmedge, gpt-oss, granite, granite-4.0, granite-4.1, grok-2, hunyuan-dense, hunyuan-moe, hunyuan-vl, kimi-k2, llama2, llama2-sys, llama2-sys-bos, llama2-sys-strip, llama3, llama4, megrez, minicpm, mistral-v1, mistral-v3, mistral-v3-tekken, mistral-v7, mistral-v7-tekken, monarch, openchat, orion, pangu-embedded, phi3, phi4, rwkv-world, seed_oss, smolvlm, solar-open, vicuna, vicuna-orca, yandex, zephyr
**Default:** (from model)

## 101. `--chat-template-file`
**Group:** Chat / Template
**Description:** Custom Jinja chat template from file
**Control:** file picker
**Values:** file path
**Default:** (from model)

## 102. `--chat-template-kwargs`
**Group:** Chat / Template
**Description:** Additional params for JSON template parser
**Control:** text input
**Values:** JSON object string
**Default:** (none)

## 103. `--skip-chat-parsing`
**Group:** Chat / Template
**Description:** Force pure content parser even with Jinja template
**Control:** checkbox
**Values:** on/off
**Default:** off

## 104. `--prefill-assistant`
**Group:** Chat / Template
**Description:** Prefill assistant response if last message is assistant
**Control:** checkbox
**Values:** on/off
**Default:** on

## 105. `--reasoning-budget-message`
**Group:** Chat / Template
**Description:** Message injected when reasoning budget exhausted
**Control:** text input
**Values:** free text
**Default:** (none)

## 106. `--log-file`
**Group:** Debug / logging
**Description:** Log to file
**Control:** file picker
**Values:** file path
**Default:** (none)

## 107. `--log-verbosity`
**Group:** Debug / logging
**Description:** Verbosity threshold
**Control:** dropdown
**Values:** 0=generic, 1=error, 2=warning, 3=info, 4=trace, 5=debug
**Default:** 3

## 108. `--log-prefix`
**Group:** Debug / logging
**Description:** Enable prefix in log messages
**Control:** checkbox
**Values:** on/off
**Default:** off

## 109. `--log-timestamps`
**Group:** Debug / logging
**Description:** Enable timestamps in log messages
**Control:** checkbox
**Values:** on/off
**Default:** off

## 110. `--log-prompts-dir`
**Group:** Debug / logging
**Description:** Log prompts to directory (debug)
**Control:** text input
**Values:** directory path
**Default:** (disabled)

## 111. `--offline`
**Group:** Debug / logging
**Description:** Offline mode: force cache, prevent network access
**Control:** checkbox
**Values:** on/off
**Default:** off

## 112. `--spec-draft-n-max`
**Group:** Speculative decoding
**Description:** Tokens to draft for speculative decoding
**Control:** spinbox (int)
**Values:** 1 to 256
**Default:** 3

## 113. `--spec-draft-n-min`
**Group:** Speculative decoding
**Description:** Min draft tokens for speculative decoding
**Control:** spinbox (int)
**Values:** 0 to 256
**Default:** 0

## 114. `--spec-type`
**Group:** Speculative decoding
**Description:** Speculative decoding type(s)
**Control:** dropdown (multi-select)
**Values:** none, draft-simple, draft-eagle3, draft-mtp, ngram-simple, ngram-map-k, ngram-map-k4v, ngram-mod, ngram-cache
**Default:** none

## 115. `--spec-draft-model`
**Group:** Speculative decoding
**Description:** Draft model path
**Control:** file picker
**Values:** file path
**Default:** (none)

## 116. `--spec-draft-hf`
**Group:** Speculative decoding
**Description:** HF repo for draft model
**Control:** text input
**Values:** user/model[:quant]
**Default:** (none)

## 117. `--spec-draft-threads`
**Group:** Speculative decoding
**Description:** Threads for draft model
**Control:** spinbox (int)
**Values:** 0 to 256
**Default:** same as --threads

## 118. `--spec-draft-ngl`
**Group:** Speculative decoding
**Description:** GPU layers for draft model
**Control:** dropdown
**Values:** number, auto, all
**Default:** auto

## 119. `--spec-draft-device`
**Group:** Speculative decoding
**Description:** Devices for draft model
**Control:** text input
**Values:** comma-separated device names
**Default:** (none)

## 120. `--spec-draft-p-split`
**Group:** Speculative decoding
**Description:** Speculative decoding split probability
**Control:** slider (float)
**Values:** 0.0 to 1.0
**Default:** 0.10

## 121. `--spec-draft-p-min`
**Group:** Speculative decoding
**Description:** Min speculative decoding probability (greedy)
**Control:** slider (float)
**Values:** 0.0 to 1.0
**Default:** 0.00

## 122. `--spec-draft-backend-sampling`
**Group:** Speculative decoding
**Description:** Offload draft sampling to backend
**Control:** checkbox
**Values:** on/off
**Default:** on

## 123. `--spec-ngram-mod-n-min`
**Group:** Speculative decoding
**Description:** Min ngram tokens for ngram-mod speculative decoding
**Control:** spinbox (int)
**Values:** 1 to 256
**Default:** 48

## 124. `--spec-ngram-mod-n-max`
**Group:** Speculative decoding
**Description:** Max ngram tokens for ngram-mod speculative decoding
**Control:** spinbox (int)
**Values:** 1 to 256
**Default:** 64

## 125. `--spec-ngram-mod-n-match`
**Group:** Speculative decoding
**Description:** Ngram-mod lookup length
**Control:** spinbox (int)
**Values:** 1 to 256
**Default:** 24

## 126. `--spec-ngram-simple-size-n`
**Group:** Speculative decoding
**Description:** Ngram size N for ngram-simple (lookup length)
**Control:** spinbox (int)
**Values:** 1 to 256
**Default:** 12

## 127. `--spec-ngram-simple-size-m`
**Group:** Speculative decoding
**Description:** Ngram size M for ngram-simple (draft length)
**Control:** spinbox (int)
**Values:** 1 to 256
**Default:** 48

## 128. `--spec-ngram-simple-min-hits`
**Group:** Speculative decoding
**Description:** Min hits for ngram-simple
**Control:** spinbox (int)
**Values:** 1 to 256
**Default:** 1

## 129. `--pooling`
**Group:** General / Miscellaneous
**Description:** Pooling type for embeddings
**Control:** dropdown
**Values:** none, mean, cls, last, rank
**Default:** (model default)

## 130. `--special`
**Group:** General / Miscellaneous
**Description:** Special tokens output enabled
**Control:** checkbox
**Values:** on/off
**Default:** off

## 131. `--warmup`
**Group:** General / Miscellaneous
**Description:** Perform warmup with empty run
**Control:** checkbox
**Values:** on/off
**Default:** on

## 132. `--spm-infill`
**Group:** General / Miscellaneous
**Description:** Use Suffix/Prefix/Middle pattern for infill
**Control:** checkbox
**Values:** on/off
**Default:** off

## 133. `--reverse-prompt`
**Group:** General / Miscellaneous
**Description:** Halt generation at this prompt
**Control:** text input
**Values:** free text
**Default:** (none)

## 134. `--tags`
**Group:** General / Miscellaneous
**Description:** Model tags (informational)
**Control:** text input
**Values:** comma-separated strings
**Default:** (none)

## 135. `--embd-normalize`
**Group:** General / Miscellaneous
**Description:** Normalisation for embeddings
**Control:** dropdown
**Values:** -1=none, 0=max abs int16, 1=taxicab, 2=euclidean, >2=p-norm
**Default:** 2

## 136. `--sleep-idle-seconds`
**Group:** General / Miscellaneous
**Description:** Seconds of idleness before server sleeps
**Control:** spinbox (int)
**Values:** -1 to 86400, -1=disabled
**Default:** -1

## 137. `--tts-use-guide-tokens`
**Group:** General / Miscellaneous
**Description:** Use guide tokens to improve TTS word recall
**Control:** checkbox
**Values:** on/off
**Default:** off

---

## Notes

- Options #112-128 replace deprecated `--draft`, `--draft-min`, `--spec-ngram-size-n`, `--spec-ngram-size-m`, `--spec-ngram-min-hits` which are in the current catalog but removed by the binary.
- Draft model CPU/thread/polling variants were omitted as they mirror main config with "same as" defaults.
- Preset model shortcuts (`--fim-qwen-*`, `--gpt-oss-*`, `--vision-gemma-*`, `--embd-gemma-default`, `--spec-default`) were excluded as they auto-download weights.
