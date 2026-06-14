---
title: "Generate semantic commit messages"
tool: claude-code
backend: ollama
model: qwen3-coder:30b
tags: [git, commits, conventional-commits, changelog]
tested: false
no_think: recommended
---

# Generate Semantic Commit Messages

Use this after staging changes to get properly formatted Conventional Commits
based on the actual diff — not guesses. Claude Code will read the real diff,
understand what changed and why, and produce ready-to-run commit commands.

Best for: messy staged changes that need clean commit messages, splitting
a large diff into logical commits, or enforcing Conventional Commits on a team.

---

## Prompt (English)

> You are a senior engineer with obsessive git hygiene. Your job is to
> analyze the current staged changes and produce clean, accurate,
> Conventional Commits-formatted commit messages that reflect exactly
> what changed and why.
>
> ---
>
> **Phase 1 — Read the diff**
> 1. Run `git status` to see what is staged and what is not.
> 2. Run `git diff --staged` to read the full staged diff.
> 3. Run `git log --oneline -10` to understand the recent commit history
>    and match the tone, scope naming and granularity already used.
> 4. If there are unstaged changes alongside staged ones, note them —
>    they may belong to the same logical unit.
>
> Do not write any commits yet.
>
> ---
>
> **Phase 2 — Analyze**
> After reading the diff:
> 1. Group the changes into logical units.
>    A logical unit = one cohesive change with a single reason to exist.
>    Examples:
>    - Adding a new function and its call site → one unit
>    - Fixing a bug in file A and an unrelated bug in file B → two units
>    - Updating a dependency and fixing a breaking change it caused → two units
>      (one `chore`, one `fix`)
> 2. For each logical unit, identify:
>    - Type: what kind of change is it
>    - Scope: what part of the codebase does it affect
>    - Description: what changed, in imperative mood
>    - Body (optional): why it changed, if not obvious from the description
>    - Breaking change (if any): note with `BREAKING CHANGE:` in the footer
>
> ---
>
> **Conventional Commits reference**
>
> Format:
> ```
> type(scope): short description
>
> [optional body — why, not what]
>
> [optional footer — BREAKING CHANGE, closes #issue]
> ```
>
> Types:
> | Type | Use when |
> |---|---|
> | `feat` | A new feature visible to the user or API consumer |
> | `fix` | A bug fix |
> | `refactor` | Code change that is neither a feature nor a bug fix |
> | `chore` | Build process, dependencies, tooling, config |
> | `docs` | Documentation only |
> | `style` | Formatting, whitespace — no logic change |
> | `test` | Adding or fixing tests |
> | `perf` | Performance improvement |
> | `ci` | CI/CD pipeline changes |
>
> Rules:
> - Description: imperative mood, lowercase, no period at end, max 72 chars
> - Scope: lowercase, short, matches the module/layer/component affected
>   (e.g. `auth`, `ui`, `api`, `config`, `db`, `commands`)
> - Body: explain the WHY, not the WHAT (the diff already shows the what)
> - One type per commit — never mix `feat` and `fix` in the same commit
>
> ---
>
> **Phase 3 — Output**
> Produce the output in this exact format:
>
> For each logical unit found:
>
> ---
> **Commit [N]**
> Files: `file1.rs`, `file2.js`
> Rationale: [one sentence explaining why this is a separate commit]
>
> ```bash
> git add file1.rs file2.js
> git commit -m "type(scope): description"
> ```
>
> *(include body/footer only if genuinely needed)*
> ```bash
> git add file1.rs file2.js
> git commit -m "type(scope): description" -m "Body explaining the why."
> ```
> ---
>
> After all commits, provide:
> - A one-line summary of the full changeset
> - A warning if the staged changes are too mixed to split cleanly,
>   with a suggestion to use `git add -p` to re-stage selectively
>
> ---
>
> **Rules**
> - Never invent changes that are not in the diff.
> - Never combine unrelated changes into one commit to keep the list short.
> - If a change is truly trivial (e.g. fix a typo in a comment),
>   group it with the nearest related commit rather than making a
>   one-word commit that pollutes the log.
> - If you cannot determine the scope confidently, use the filename
>   or top-level folder as scope rather than guessing.
> - Do not run `git commit` automatically — output the commands for
>   me to review and run manually.

---

## Prompt (Español)

> Eres un ingeniero senior con higiene git obsesiva. Tu trabajo es
> analizar los cambios staged actuales y producir mensajes de commit
> limpios, precisos y en formato Conventional Commits que reflejen
> exactamente qué cambió y por qué.
>
> ---
>
> **Fase 1 — Leer el diff**
> 1. Ejecuta `git status` para ver qué está staged y qué no.
> 2. Ejecuta `git diff --staged` para leer el diff staged completo.
> 3. Ejecuta `git log --oneline -10` para entender el historial reciente
>    y ajustarte al tono, nombrado de scopes y granularidad ya usados.
> 4. Si hay cambios unstaged junto a los staged, anótalos —
>    pueden pertenecer a la misma unidad lógica.
>
> No escribas ningún commit todavía.
>
> ---
>
> **Fase 2 — Análisis**
> Tras leer el diff:
> 1. Agrupa los cambios en unidades lógicas.
>    Una unidad lógica = un cambio cohesivo con una sola razón de existir.
>    Ejemplos:
>    - Añadir una función nueva y su call site → una unidad
>    - Arreglar un bug en el archivo A y otro no relacionado en B → dos unidades
>    - Actualizar una dependencia y arreglar un breaking change que causó → dos unidades
>      (un `chore`, un `fix`)
> 2. Para cada unidad lógica, identifica:
>    - Tipo: qué clase de cambio es
>    - Scope: qué parte del código afecta
>    - Descripción: qué cambió, en modo imperativo
>    - Body (opcional): por qué cambió, si no es obvio por la descripción
>    - Breaking change (si aplica): indicar con `BREAKING CHANGE:` en el footer
>
> ---
>
> **Referencia Conventional Commits**
>
> Formato:
> ```
> type(scope): descripción corta
>
> [body opcional — el por qué, no el qué]
>
> [footer opcional — BREAKING CHANGE, closes #issue]
> ```
>
> Tipos:
> | Tipo | Cuándo usarlo |
> |---|---|
> | `feat` | Nueva funcionalidad visible al usuario o consumidor de API |
> | `fix` | Corrección de bug |
> | `refactor` | Cambio de código que no es ni feature ni bug fix |
> | `chore` | Build, dependencias, tooling, configuración |
> | `docs` | Solo documentación |
> | `style` | Formato, espaciado — sin cambio de lógica |
> | `test` | Añadir o arreglar tests |
> | `perf` | Mejora de rendimiento |
> | `ci` | Cambios en pipeline CI/CD |
>
> Reglas:
> - Descripción: modo imperativo, minúsculas, sin punto al final, máx 72 chars
> - Scope: minúsculas, corto, refleja el módulo/capa/componente afectado
>   (e.g. `auth`, `ui`, `api`, `config`, `db`, `commands`)
> - Body: explica el POR QUÉ, no el QUÉ (el diff ya muestra el qué)
> - Un tipo por commit — nunca mezcles `feat` y `fix` en el mismo commit
>
> ---
>
> **Fase 3 — Output**
> Produce el output en este formato exacto:
>
> Por cada unidad lógica encontrada:
>
> ---
> **Commit [N]**
> Archivos: `archivo1.rs`, `archivo2.js`
> Razonamiento: [una frase explicando por qué es un commit separado]
>
> ```bash
> git add archivo1.rs archivo2.js
> git commit -m "type(scope): descripción"
> ```
>
> *(incluir body/footer solo si es genuinamente necesario)*
> ```bash
> git add archivo1.rs archivo2.js
> git commit -m "type(scope): descripción" -m "Body explicando el por qué."
> ```
> ---
>
> Tras todos los commits, incluye:
> - Un resumen de una línea del changeset completo
> - Un aviso si los cambios staged están demasiado mezclados para dividirse
>   limpiamente, con sugerencia de usar `git add -p` para re-stagear
>   de forma selectiva
>
> ---
>
> **Reglas**
> - Nunca inventes cambios que no estén en el diff.
> - Nunca combines cambios no relacionados en un commit para acortar la lista.
> - Si un cambio es verdaderamente trivial (e.g. typo en un comentario),
>   agrúpalo con el commit relacionado más cercano en lugar de hacer un
>   commit de una palabra que ensucie el log.
> - Si no puedes determinar el scope con confianza, usa el nombre del archivo
>   o carpeta de primer nivel como scope en lugar de adivinar.
> - No ejecutes `git commit` automáticamente — muestra los comandos para
>   que yo los revise y ejecute manualmente.

---

## Notes

- The **"do not run `git commit` automatically"** rule is critical —
  you always want to read the proposed messages before they land in
  the history. A wrong commit message is annoying to fix after the fact.
- The **`git add -p` warning** is one of the most useful outputs of this
  prompt — it tells you when your staged changes are too mixed and need
  to be re-staged more carefully before committing.
- The **`git log --oneline -10` step** makes the model match your existing
  commit style instead of imposing its own — scope naming in particular
  tends to drift if the model doesn't read the history first.
- `/no_think` recommended — this is pattern-matching and formatting,
  not deep architectural reasoning.
- No minimum `num_ctx` requirement — works well even at 8192 for normal diffs.
  For very large diffs (500+ lines), use at least `16384`.
- Tested on: any project with git initialized.
