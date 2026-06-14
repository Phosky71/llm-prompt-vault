# Claude Code · Ollama Local

Prompts for Claude Code CLI running against a local model via Ollama.

## Tested setup

- **Tool**: Claude Code CLI
- **Backend**: Ollama
- **Model**: `qwen3-coder:30b`
- **OS**: Windows 11

## Recommended Modelfile

Create a custom model with this config for best results:

```modelfile
FROM qwen3-coder:30b
PARAMETER num_ctx 32768
PARAMETER temperature 0.7
PARAMETER top_p 0.8
PARAMETER top_k 20
PARAMETER repeat_penalty 1.05
```

```bash
ollama create qwen3-coder-claude -f Modelfile
```

## Recommended Ollama env vars

```powershell
setx OLLAMA_NUM_GPU_LAYERS "999"
setx OLLAMA_NUM_BATCH "512"
setx OLLAMA_NUM_THREADS "6"
setx OLLAMA_FLASH_ATTENTION "1"
setx OLLAMA_KV_CACHE_TYPE "q4_0"
setx OLLAMA_MAX_LOADED_MODELS "1"
setx OLLAMA_NUM_PARALLEL "1"
setx OLLAMA_CONTEXT_LENGTH "32768"
```

## Categories

| Folder | Description |
|---|---|
| `debug/` | Find and fix bugs in existing code |
| `review/` | Analyze projects without modifying anything |
| `features/` | Add new functionality to an existing project |
| `refactor/` | Improve structure without changing behavior |
| `docs/` | Generate documentation |
| `git/` | Git-related tasks |
