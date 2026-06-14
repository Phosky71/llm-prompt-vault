# 🔨 llm-prompt-vault

> A growing collection of structured prompts for AI tools and local LLMs.
> Organized by tool · Tested in real projects · Ready to copy-paste.

## Structure

| Folder | Tool | Mode |
|---|---|---|
| `claudecode-ollama-local/` | Claude Code CLI | Local model via Ollama |

## How to use

1. Browse to the folder matching your tool and setup
2. Pick a prompt by category and use case
3. Replace `[placeholder]` fields with your actual values
4. Paste directly into the tool's input

## Note on `/no_think`

Some prompts include a `/no_think` recommendation. Add it at the very
beginning of the prompt when using `qwen3-coder:30b` locally and speed
is a priority. It disables the internal reasoning chain and can cut
response time significantly.
