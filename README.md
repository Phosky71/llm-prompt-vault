# 🔨 llm-prompt-vault

> A growing collection of structured prompts for AI tools and local LLMs.
> Organized by tool · Tested in real projects · Ready to copy-paste.

---

## Structure
prompt-forge/
├── claudecode-ollama-local/ # Claude Code CLI via Ollama (local model)
│ ├── debug/ # Find and fix bugs
│ ├── review/ # Read-only project analysis
│ ├── features/ # Add new functionality
│ ├── refactor/ # Improve code structure
│ ├── docs/ # Generate documentation
│ └── git/ # Git workflow tasks
└── templates/ # Blank template to create new prompts

text

---

## How to use a prompt

1. Navigate to the folder matching your tool and setup
2. Pick a prompt by category and use case
3. Read the **Notes** section first — it explains the key design decisions
4. Replace every `[placeholder]` with your actual values
5. Paste the full prompt into the tool input and run it

---

## Prompt design principles

Every prompt in this repository follows the same philosophy:

**Phases over one-shots**
Prompts are split into phases with a confirmation step before any
irreversible action. This keeps you in control and prevents the model
from making large unwanted changes based on wrong assumptions.

**Git-first**
Every prompt that modifies files uses a dedicated branch and commits
each logical change individually. Changes are always reversible.

**Explicit over implicit**
Prompts tell the model exactly what to do, what NOT to do, and in what
order. Nothing is left to interpretation — especially rules about scope,
file boundaries and behavior preservation.

**Honest output**
Prompts instruct the model to flag gaps with `⚠️ TODO` rather than
invent values. A prompt that admits uncertainty is more useful than
one that silently produces wrong output.

---

## `/no_think` flag

Some prompts recommend adding `/no_think` at the very beginning of the
prompt when using `qwen3-coder:30b` locally. This disables the internal
reasoning chain (thinking mode) and can significantly reduce response time.

| Use `/no_think` when | Avoid `/no_think` when |
|---|---|
| Structured output tasks (README, commits) | Bug analysis and debugging |
| Simple read-only tasks | Feature planning and architecture |
| Speed matters more than depth | Refactor impact analysis |

---

## Recommended model setup (Claude Code + Ollama)

### Modelfile

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

### Environment variables (Windows)

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

Restart your terminal after setting these variables.

---

## Adding a new prompt

1. Copy `templates/prompt-template.md`
2. Place it in the correct tool folder and category subfolder
3. Fill in the frontmatter and all sections
4. Set `tested: false` until you have verified it on a real project
5. Open a PR or commit directly with:
   `git commit -m "feat(claudecode-ollama-local): add [category]/[name] prompt"`

---

## Roadmap

- [ ] `claudecode-ollama-local/debug/fix-errors.md` ✅
- [ ] `claudecode-ollama-local/review/full-project-review.md` ✅
- [ ] `claudecode-ollama-local/features/add-feature.md` ✅
- [ ] `claudecode-ollama-local/refactor/improve-module.md` ✅
- [ ] `claudecode-ollama-local/docs/generate-readme.md` ✅
- [ ] `claudecode-ollama-local/git/commit-messages.md` ✅
- [ ] `claudecode-anthropic/` — prompts for Claude Code with Anthropic API
- [ ] `cursor/` — prompts for Cursor IDE
- [ ] `chatgpt/` — prompts for ChatGPT

---

## License

MIT
