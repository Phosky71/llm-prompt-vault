---
title: "Fix errors in existing app"
tool: claude-code
backend: ollama
model: qwen3-coder:30b
tags: [debug, fix, errors, stability, git]
tested: true
no_think: optional
---

# Fix Errors in Existing App

Use this when you have a broken or partially working application.
Claude Code will analyze the full codebase, identify bugs, fix them
with proper git hygiene — branch, commits per fix, final summary.

Best for: crashes, broken features, logic errors, silent failures.

---

## Prompt (English)

> You are an expert software debugger with strong git discipline.
> I have an application that is partially broken. Your job is to fix it
> and leave a clean, traceable git history of every change made.
>
> ---
>
> **Goal**
> Leave the application stable, without critical errors and with correct
> behavior. Every fix must be committed individually with a descriptive
> message. Do not introduce new features or change what already works.
>
> ---
>
> **Project context**
> - Language / framework: [e.g. Rust/Tauri backend · JS/HTML/CSS frontend]
> - Project structure: [e.g. `src-tauri/` for backend · `src/` for frontend]
> - Known issues:
>   - [Issue #1 — be specific: "clicking Add Repository does nothing, no console error"]
>   - [Issue #2]
>
> ---
>
> **Phase 1 — Analysis (do not modify or commit anything yet)**
> 1. Run `git status` and `git log --oneline -10` to understand the current state.
> 2. Explore the full project structure.
> 3. Read every relevant file — backend, frontend, config, dependencies.
> 4. Identify all bugs, logic errors, missing error handling and bad practices.
> 5. Produce a structured report:
>    - **Critical** — causes crashes or completely broken functionality
>    - **Medium** — incorrect behavior, unhandled edge cases
>    - **Low** — bad practices, minor issues, potential future problems
>    - **Working** — explicitly list what should NOT be touched
>
> After the report, stop and wait for my confirmation before proceeding.
>
> ---
>
> **Phase 2 — Git setup (before any fix)**
> 1. Create and switch to a new branch:
>    `git checkout -b fix/[short-description-of-main-issue]`
> 2. Confirm the branch is active before touching any file.
>
> ---
>
> **Phase 3 — Fixes**
> Apply fixes in order: critical first, then medium, then low.
> For each individual fix:
> 1. Edit the file(s) directly — do not just suggest changes.
> 2. Add a short inline comment where the fix was applied explaining
>    what was wrong and what changed.
> 3. Stage and commit immediately after each fix:
>    `git add <changed files>`
>    `git commit -m "fix(scope): description of what was fixed"`
> 4. Use Conventional Commits format for all messages:
>    - `fix(scope): description` for bug fixes
>    - `chore(scope): description` for config or dependency changes
>    - `refactor(scope): description` only if unavoidable for the fix
>
> Rules:
> - One commit per fix — never batch unrelated changes.
> - Do not refactor code unrelated to the bug being fixed.
> - Do not change working features, public interfaces or existing behavior.
> - If a fix requires a decision between two valid approaches,
>   stop, explain the trade-offs, and wait for my choice.
> - Maintain full compatibility with current dependencies and versions.
>
> ---
>
> **Phase 4 — Final summary**
> Once all fixes are applied:
> 1. Run `git log --oneline` and show the list of commits made.
> 2. Provide a summary table:
>    | # | File(s) changed | What was wrong | What was fixed |
>    |---|---|---|---|
> 3. List any remaining Low priority issues that were intentionally left
>    for a separate task.
> 4. Suggest next steps if relevant (e.g. "consider adding error boundary
>    to X component").

---

## Prompt (Español)

> Eres un experto en depuración de software con disciplina git rigurosa.
> Tengo una aplicación parcialmente rota. Tu trabajo es arreglarla
> y dejar un historial git limpio y trazable de cada cambio realizado.
>
> ---
>
> **Objetivo**
> Dejar la aplicación estable, sin errores críticos y con comportamiento
> correcto. Cada arreglo debe commitearse individualmente con un mensaje
> descriptivo. No introduzcas nuevas funcionalidades ni cambies lo que
> ya funciona.
>
> ---
>
> **Contexto del proyecto**
> - Lenguaje / framework: [e.g. Rust/Tauri backend · JS/HTML/CSS frontend]
> - Estructura: [e.g. `src-tauri/` para backend · `src/` para frontend]
> - Problemas conocidos:
>   - [Problema #1 — sé específico: "al pulsar Añadir Repositorio no ocurre nada, sin error en consola"]
>   - [Problema #2]
>
> ---
>
> **Fase 1 — Análisis (sin modificar ni commitear nada todavía)**
> 1. Ejecuta `git status` y `git log --oneline -10` para entender el estado actual.
> 2. Explora la estructura completa del proyecto.
> 3. Lee todos los archivos relevantes — backend, frontend, configuración, dependencias.
> 4. Identifica todos los bugs, errores lógicos, falta de manejo de errores y malas prácticas.
> 5. Genera un informe estructurado:
>    - **Crítico** — provoca crashes o funcionalidad completamente rota
>    - **Medio** — comportamiento incorrecto, casos borde no manejados
>    - **Bajo** — malas prácticas, problemas menores, problemas potenciales futuros
>    - **Funciona bien** — lista explícita de lo que NO debe tocarse
>
> Tras el informe, detente y espera mi confirmación antes de continuar.
>
> ---
>
> **Fase 2 — Preparación git (antes de cualquier arreglo)**
> 1. Crea y cambia a una nueva rama:
>    `git checkout -b fix/[descripcion-corta-del-problema-principal]`
> 2. Confirma que la rama está activa antes de tocar cualquier archivo.
>
> ---
>
> **Fase 3 — Correcciones**
> Aplica los arreglos en orden: primero críticos, luego medios, luego bajos.
> Por cada arreglo individual:
> 1. Edita los archivos directamente — no te limites a sugerir cambios.
> 2. Añade un comentario inline breve donde se aplicó el arreglo explicando
>    qué estaba mal y qué has cambiado.
> 3. Stagea y commitea inmediatamente tras cada arreglo:
>    `git add <archivos modificados>`
>    `git commit -m "fix(scope): descripción de lo corregido"`
> 4. Usa el formato Conventional Commits para todos los mensajes:
>    - `fix(scope): descripción` para correcciones de bugs
>    - `chore(scope): descripción` para cambios de config o dependencias
>    - `refactor(scope): descripción` solo si es inevitable para el arreglo
>
> Reglas:
> - Un commit por arreglo — nunca agrupes cambios no relacionados.
> - No refactorices código que no esté relacionado con el bug que se está arreglando.
> - No cambies funcionalidades que funcionen, interfaces públicas ni comportamiento existente.
> - Si un arreglo requiere elegir entre dos enfoques válidos,
>   detente, explica los trade-offs y espera mi elección.
> - Mantén compatibilidad total con las dependencias y versiones actuales.
>
> ---
>
> **Fase 4 — Resumen final**
> Una vez aplicados todos los arreglos:
> 1. Ejecuta `git log --oneline` y muestra la lista de commits realizados.
> 2. Proporciona una tabla resumen:
>    | # | Archivo(s) modificado(s) | Qué estaba mal | Qué se corrigió |
>    |---|---|---|---|
> 3. Lista los problemas de prioridad Baja que se dejaron intencionalmente
>    para una tarea separada.
> 4. Sugiere próximos pasos si es relevante.

---

## Notes

- The **two-phase approach with confirmation** is critical with local models —
  prevents large unwanted changes before you validate the analysis.
- The **git branch + per-fix commits** workflow keeps changes reversible:
  if a fix breaks something, `git revert` or `git checkout` recovers instantly.
- Add `/no_think` at the very start only for small, obvious bugs.
  For complex issues the reasoning chain significantly improves accuracy.
- Minimum recommended `num_ctx`: `32768`. For large projects: `65536`.
- The more specific the "Known issues" section, the fewer hallucinations.
- Tested on: Rust/Tauri + JS/HTML/CSS · .NET MAUI · Next.js
