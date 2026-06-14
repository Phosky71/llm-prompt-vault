# Claude Code · Ollama Local

Prompts for **Claude Code CLI** running against a local model via **Ollama**.
All prompts are designed and tested with `qwen3-coder:30b` on consumer hardware.

---

## Tested setup

| Component | Value |
|---|---|
| Tool | Claude Code CLI |
| Backend | Ollama |
| Model | `qwen3-coder:30b` |
| OS | Windows 11 |
| GPU | NVIDIA RTX 3060 12 GB VRAM |
| RAM | 32 GB |

---

## Prompts

| File | Category | What it does | `/no_think` |
|---|---|---|---|
| `debug/fix-errors.md` | Debug | Find and fix bugs with full git workflow | Optional |
| `review/full-project-review.md` | Review | Deep read-only audit of any codebase | Optional |
| `features/add-feature.md` | Features | Implement new functionality cleanly | Not recommended |
| `refactor/improve-module.md` | Refactor | Improve a module without changing behavior | Not recommended |
| `docs/generate-readme.md` | Docs | Generate a complete README from code | Recommended |
| `git/commit-messages.md` | Git | Generate Conventional Commits from staged diff | Recommended |

---

## Recommended workflow order

For a project you have never touched before:
review/full-project-review.md ← understand before touching anything

debug/fix-errors.md ← fix what is broken

refactor/improve-module.md ← clean up the worst areas

features/add-feature.md ← add new functionality

docs/generate-readme.md ← document when stable

text

`git/commit-messages.md` can be used at any point after staging changes.

---

## Setup

### 1. Create the optimized model

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

### 2. Set environment variables (Windows — run once, then restart terminal)

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

### 3. Point Claude Code to Ollama

```bash
export ANTHROPIC_BASE_URL=http://localhost:11434
export ANTHROPIC_API_KEY=ollama
claude --model qwen3-coder-claude
```

---

## Notes

- All prompts use a **phase-based structure** with a confirmation step
  before any file is modified. Never skip the confirmation — it is the
  main safeguard against unwanted changes with local models.
- If the model seems slow, add `/no_think` at the very start of the prompt
  (only for prompts where it is marked as Optional or Recommended).
- If you get context length errors, increase `num_ctx` to `65536` in the
  Modelfile and `OLLAMA_CONTEXT_LENGTH` accordingly.
