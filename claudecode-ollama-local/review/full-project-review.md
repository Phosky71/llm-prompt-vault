---
title: "Full project review (read-only)"
tool: claude-code
backend: ollama
model: qwen3-coder:30b
tags: [review, analysis, read-only, audit, first-contact]
tested: true
no_think: optional
---

# Full Project Review (Read-Only)

Use this as the **first thing you run on any project** — whether it's yours
or someone else's. Claude Code will do a deep read of the entire codebase
and produce a structured audit report without touching a single file.

Best for: onboarding to an unfamiliar codebase, pre-refactor audit,
spotting hidden bugs before they surface, technical debt mapping.

**This prompt makes zero modifications. No files are created, edited or deleted.**

---

## Prompt (English)

> You are a senior software engineer doing a full audit of this project.
> Your only job right now is to read, understand and report.
> Do NOT create, modify or delete any file under any circumstance.
>
> ---
>
> **Goal**
> Produce a complete, honest and actionable audit report of this codebase.
> I need to understand what the project does, how it is structured, what
> works, what is broken, and what will become a problem in the future.
>
> ---
>
> **Phase 1 — Reconnaissance**
> Start by running these commands to understand the current state:
> 1. `git log --oneline -20` — recent history
> 2. `git status` — uncommitted changes
> 3. `git branch -a` — existing branches
>
> Then explore the full project structure before reading any file in detail.
> Map out:
> - Root directory layout
> - Entry points (main file, index, Program.cs, main.rs, etc.)
> - Configuration files (package.json, Cargo.toml, .csproj, .env, etc.)
> - Frontend vs backend separation if applicable
> - Test coverage if any tests exist
>
> ---
>
> **Phase 2 — Deep read**
> Read every relevant source file. Prioritize in this order:
> 1. Entry points and bootstrapping code
> 2. Core business logic
> 3. Data models and database layer
> 4. API layer or IPC layer (commands, routes, handlers)
> 5. Frontend / UI logic
> 6. Utilities and shared modules
> 7. Configuration and environment handling
>
> As you read, take notes. Do not write anything to disk.
>
> ---
>
> **Phase 3 — Report**
> Produce the full audit report using this exact structure:
>
> ### 1. Project Overview
> - What this application does (2-3 sentences max)
> - Tech stack with versions if visible
> - Overall code quality impression (be honest)
>
> ### 2. Architecture
> - How the project is structured
> - How frontend and backend communicate (if applicable)
> - Data flow: from user action to data persistence and back
> - Any notable architectural decisions (good or bad)
>
> ### 3. Critical Issues 🔴
> Issues that cause crashes, data loss, broken core functionality,
> or serious security problems.
> For each issue:
> - File and line number
> - What is wrong
> - Why it is dangerous
> - Suggested fix (brief)
>
> ### 4. Medium Issues 🟡
> Incorrect behavior, unhandled edge cases, missing validations,
> broken error handling.
> Same format as Critical Issues.
>
> ### 5. Low Issues 🟢
> Bad practices, code smells, dead code, inconsistencies, minor
> inefficiencies that do not affect current behavior.
>
> ### 6. What Works Well ✅
> Explicitly list parts of the codebase that are solid and should
> not be touched unless strictly necessary.
>
> ### 7. Technical Debt Map
> Areas with the highest accumulated debt, ordered by priority.
> Be specific — name files and modules, not just "the backend".
>
> ### 8. Recommended Next Steps
> An ordered list of what to tackle first, based on severity and effort.
> Format:
> | Priority | Task | Effort | Impact |
> |---|---|---|---|
>
> ---
>
> **Final rule**
> If at any point during reading you feel the urge to fix something —
> do not. Write it in the report instead. Zero modifications. Zero commits.

---

## Prompt (Español)

> Eres un ingeniero de software senior realizando una auditoría completa
> de este proyecto. Tu único trabajo ahora mismo es leer, entender e informar.
> Bajo ninguna circunstancia crees, modifiques o elimines ningún archivo.
>
> ---
>
> **Objetivo**
> Producir un informe de auditoría completo, honesto y accionable de este
> código. Necesito entender qué hace el proyecto, cómo está estructurado,
> qué funciona, qué está roto y qué se convertirá en un problema en el futuro.
>
> ---
>
> **Fase 1 — Reconocimiento**
> Empieza ejecutando estos comandos para entender el estado actual:
> 1. `git log --oneline -20` — historial reciente
> 2. `git status` — cambios sin commitear
> 3. `git branch -a` — ramas existentes
>
> Luego explora la estructura completa del proyecto antes de leer ningún
> archivo en detalle. Mapea:
> - Distribución del directorio raíz
> - Puntos de entrada (archivo main, index, Program.cs, main.rs, etc.)
> - Archivos de configuración (package.json, Cargo.toml, .csproj, .env, etc.)
> - Separación frontend/backend si aplica
> - Cobertura de tests si existen
>
> ---
>
> **Fase 2 — Lectura en profundidad**
> Lee todos los archivos fuente relevantes. Prioriza en este orden:
> 1. Puntos de entrada y código de arranque
> 2. Lógica de negocio principal
> 3. Modelos de datos y capa de base de datos
> 4. Capa API o IPC (comandos, rutas, handlers)
> 5. Lógica de frontend / UI
> 6. Utilidades y módulos compartidos
> 7. Configuración y manejo de variables de entorno
>
> Mientras lees, toma notas. No escribas nada en disco.
>
> ---
>
> **Fase 3 — Informe**
> Produce el informe de auditoría completo usando exactamente esta estructura:
>
> ### 1. Descripción del proyecto
> - Qué hace esta aplicación (máximo 2-3 frases)
> - Stack tecnológico con versiones si son visibles
> - Impresión general de la calidad del código (sé honesto)
>
> ### 2. Arquitectura
> - Cómo está estructurado el proyecto
> - Cómo se comunican frontend y backend (si aplica)
> - Flujo de datos: desde la acción del usuario hasta la persistencia y de vuelta
> - Decisiones arquitectónicas destacables (buenas o malas)
>
> ### 3. Problemas críticos 🔴
> Problemas que provocan crashes, pérdida de datos, funcionalidad principal
> rota o problemas graves de seguridad.
> Por cada problema:
> - Archivo y número de línea
> - Qué está mal
> - Por qué es peligroso
> - Arreglo sugerido (breve)
>
> ### 4. Problemas medios 🟡
> Comportamiento incorrecto, casos borde no manejados, validaciones ausentes,
> manejo de errores roto.
> Mismo formato que Problemas críticos.
>
> ### 5. Problemas bajos 🟢
> Malas prácticas, code smells, código muerto, inconsistencias, ineficiencias
> menores que no afectan al comportamiento actual.
>
> ### 6. Lo que funciona bien ✅
> Lista explícita de las partes del código que son sólidas y no deben
> tocarse salvo que sea estrictamente necesario.
>
> ### 7. Mapa de deuda técnica
> Áreas con mayor deuda acumulada, ordenadas por prioridad.
> Sé específico — nombra archivos y módulos, no solo "el backend".
>
> ### 8. Próximos pasos recomendados
> Lista ordenada de qué abordar primero, basada en severidad y esfuerzo.
> Formato:
> | Prioridad | Tarea | Esfuerzo | Impacto |
> |---|---|---|---|
>
> ---
>
> **Regla final**
> Si en algún momento durante la lectura sientes el impulso de arreglar algo —
> no lo hagas. Escríbelo en el informe. Cero modificaciones. Cero commits.

---

## Notes

- Run this **before** `debug/fix-errors.md` on any unfamiliar project —
  it gives you the full picture before anything gets changed.
- The "What Works Well" section is as important as the bug list —
  it prevents Claude Code from "fixing" things that don't need fixing.
- `/no_think` acceptable only for very small projects (< 10 files).
  For anything real, the reasoning chain produces a significantly
  better and more complete report.
- Minimum recommended `num_ctx`: `32768`.
  For large projects with many files: `65536`.
- The report output is long — expect Claude Code to take several minutes
  on a real project with a local 30B model.
- Tested on: Rust/Tauri + JS/HTML/CSS · .NET MAUI · Next.js
