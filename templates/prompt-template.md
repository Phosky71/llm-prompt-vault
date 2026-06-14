---
title: ""
tool: claude-code
backend: ollama
model: qwen3-coder:30b
tags: []
tested: false
no_think: false
---

# [Prompt Title]

One paragraph describing what this prompt does, when to use it and
what problem it solves. Be specific — "use this when X" is more useful
than "use this to do Y".

Best for: [specific scenarios, separated by commas].

---

## Prompt (English)

> [Your prompt here.]
>
> Use blockquote format for the entire prompt body.
> Each major section should have a bold header:
>
> ---
>
> **Goal**
> [What the agent must achieve by the end.]
>
> ---
>
> **Context**
> - Key: [Value — use placeholders like [e.g. something] for user-filled fields]
>
> ---
>
> **Phase 1 — [Name]**
> [Steps the agent must follow before doing anything irreversible.]
> [Always end analysis phases with: "Stop and wait for my confirmation."]
>
> ---
>
> **Phase 2 — [Name]**
> [The main action phase. Include git setup if the prompt modifies files.]
>
> ---
>
> **Rules**
> - [Hard constraints the agent must never violate.]
> - [Use "do NOT" for non-negotiable rules.]

---

## Prompt (Español)

> [Traducción exacta del prompt en inglés.]
>
> Mantén el mismo formato, estructura y fases.
> Traduce los headers en negrita también.
> No adaptes ni simplifiques el contenido — traducción fiel, no resumen.

---

## Notes

- Explain the most important rule or design decision in this prompt
  and why it exists.
- `/no_think` recommendation with a clear reason:
  - Recommended: formatting, structured output, simple read tasks
  - Optional: medium complexity tasks where speed matters more than depth
  - Not recommended: architecture decisions, bug analysis, feature planning
- Minimum recommended `num_ctx`: [value]
- Tested on: [frameworks / languages, or "not yet tested"]
