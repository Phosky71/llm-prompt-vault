---
title: "Fix errors in existing app"
tool: claude-code
backend: ollama
model: qwen3-coder:30b
tags: [debug, fix, errors, stability]
tested: true
no_think: optional
---

# Fix Errors in Existing App

Use this when you have a broken or partially working application.
Claude Code will analyze the full codebase, identify bugs and fix them
without touching anything that already works.

Best for: crashes, broken features, logic errors, silent failures.

---

## Prompt (English)

> You are an expert software debugger. I have an application that is
> partially broken. Your job is to fix it.
>
> ---
>
> **Goal**
> Leave the application stable, without critical errors and with correct
> behavior. Do not introduce new features or change what already works.
>
> ---
>
> **Project context**
> - Language / framework: [e.g. Rust/Tauri backend · JS/HTML/CSS frontend]
> - Project structure: [e.g. `src-tauri/` for backend · `src/` for frontend]
> - Known issues:
>   - [Issue #1 — be as specific as possible, e.g. "clicking Add Repository does nothing and no error appears in console"]
>   - [Issue #2]
>
> ---
>
> **Phase 1 — Analysis (do not modify anything yet)**
> 1. Explore the full project structure.
> 2. Read every relevant file — backend, frontend, config, dependencies.
> 3. Identify all bugs, logic errors, missing error handling and bad practices.
> 4. Produce a structured report:
>    - **Critical** (causes crashes or broken functionality)
>    - **Medium** (incorrect behavior, edge cases)
>    - **Low** (bad practices, minor issues)
>
> After the report, stop and wait for my confirmation before proceeding.
>
> ---
>
> **Phase 2 — Fixes (only after confirmation)**
> 1. Fix all critical and medium issues found.
> 2. Edit the files directly — do not just suggest changes.
> 3. For each fix, add a short inline comment explaining what was wrong
>    and what you changed.
> 4. Do not refactor code that is unrelated to the bugs.
> 5. Do not change working features, public interfaces or existing behavior.
>
> ---
>
> **Restrictions**
> - Prioritize stability over optimization.
> - One fix at a time — do not batch unrelated changes.
> - If a fix requires a decision (e.g. two valid approaches), explain
>   the trade-offs and ask before proceeding.
> - Maintain full compatibility with the current dependencies and versions.

---

## Prompt (Español)

> Eres un experto en depuración de software. Tengo una aplicación que
> está parcialmente rota. Tu trabajo es arreglarla.
>
> ---
>
> **Objetivo**
> Dejar la aplicación estable, sin errores críticos y con comportamiento
> correcto. No introduzcas nuevas funcionalidades ni cambies lo que ya
> funciona.
>
> ---
>
> **Contexto del proyecto**
> - Lenguaje / framework: [e.g. Rust/Tauri backend · JS/HTML/CSS frontend]
> - Estructura del proyecto: [e.g. `src-tauri/` para backend · `src/` para frontend]
> - Problemas conocidos:
>   - [Problema #1 — sé lo más específico posible, e.g. "al pulsar Añadir Repositorio no ocurre nada y no aparece ningún error en consola"]
>   - [Problema #2]
>
> ---
>
> **Fase 1 — Análisis (sin modificar nada todavía)**
> 1. Explora la estructura completa del proyecto.
> 2. Lee todos los archivos relevantes — backend, frontend, configuración, dependencias.
> 3. Identifica todos los bugs, errores lógicos, falta de manejo de errores y malas prácticas.
> 4. Genera un informe estructurado:
>    - **Crítico** (provoca crashes o funcionalidad rota)
>    - **Medio** (comportamiento incorrecto, casos borde)
>    - **Bajo** (malas prácticas, problemas menores)
>
> Tras el informe, detente y espera mi confirmación antes de continuar.
>
> ---
>
> **Fase 2 — Correcciones (solo tras confirmación)**
> 1. Corrige todos los problemas críticos y medios encontrados.
> 2. Edita los archivos directamente — no te limites a sugerir cambios.
> 3. Por cada corrección, añade un comentario inline breve explicando
>    qué estaba mal y qué has cambiado.
> 4. No refactorices código que no esté relacionado con los bugs.
> 5. No cambies funcionalidades que funcionen, interfaces públicas ni
>    el comportamiento existente.
>
> ---
>
> **Restricciones**
> - Prioriza estabilidad sobre optimización.
> - Un arreglo cada vez — no agrupes cambios no relacionados.
> - Si un arreglo requiere una decisión (e.g. dos enfoques válidos),
>   explica los trade-offs y pregunta antes de proceder.
> - Mantén compatibilidad total con las dependencias y versiones actuales.

---

## Notes

- The **two-phase approach** (analyze → confirm → fix) is critical with local
  models: it prevents large unwanted changes and keeps you in control.
- Add `/no_think` at the very start only if the project is small and simple —
  for complex bugs the reasoning chain significantly improves accuracy.
- Minimum recommended `num_ctx`: `32768`. For large projects use `65536`.
- The more specific the "Known issues" section, the fewer hallucinations.
- Tested on: Rust/Tauri + JS/HTML/CSS · .NET MAUI · Next.js
