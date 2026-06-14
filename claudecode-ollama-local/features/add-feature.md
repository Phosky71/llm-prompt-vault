---
title: "Add a new feature to an existing project"
tool: claude-code
backend: ollama
model: qwen3-coder:30b
tags: [feature, development, integration, git]
tested: false
no_think: not recommended
---

# Add a New Feature

Use this to implement a new feature in an existing project while respecting
the current architecture, code style and git workflow.

Best for: adding functionality that integrates with existing code —
new UI components, new API endpoints, new backend commands, new integrations.

**Always run `full-project-review.md` first if the codebase is unfamiliar.**

---

## Prompt (English)

> You are a senior software engineer implementing a new feature on an
> existing production codebase. Your job is to deliver clean, working,
> well-committed code that fits naturally into the project as it is.
>
> ---
>
> **Feature to implement**
> [Describe the feature clearly and completely. Include:
> - What it does from the user's perspective
> - Where it lives in the UI / API / backend
> - Any specific behavior, edge cases or validation rules
> - What it should NOT do]
>
> ---
>
> **Project context**
> - Language / framework: [e.g. Rust/Tauri backend · JS/HTML/CSS frontend]
> - Project structure: [e.g. `src-tauri/` for backend · `src/` for frontend]
> - Related existing code: [e.g. "see AuthService.cs" · "similar to the /api/users route" · "follows the pattern in commands.rs"]
> - Constraints: [e.g. "no new dependencies" · "must work offline" · "keep existing API contract"]
>
> ---
>
> **Phase 1 — Understanding (do not write any code yet)**
> 1. Run `git log --oneline -10` and `git status` to understand current state.
> 2. Read all files relevant to the feature area.
> 3. Identify exactly where the new code will live — files, functions,
>    modules, routes or components that need to be created or extended.
> 4. Detect any existing patterns, conventions or abstractions you must follow
>    (naming, error handling style, state management, IPC pattern, etc.).
> 5. Produce a brief implementation plan:
>    - List of files to create (if any)
>    - List of files to modify (with the specific change per file)
>    - Any potential side effects on existing functionality
>    - Open questions or decisions that need my input
>
> Stop here and wait for my confirmation before writing any code.
> If you have open questions, ask them now — do not assume.
>
> ---
>
> **Phase 2 — Git setup**
> 1. Create and switch to a new branch:
>    `git checkout -b feat/[short-feature-name]`
> 2. Confirm the branch is active.
>
> ---
>
> **Phase 3 — Implementation**
> Implement the feature following the approved plan exactly.
>
> Rules:
> - Follow the existing code style, naming conventions and architecture.
> - Do not introduce new dependencies unless explicitly approved.
> - Do not refactor unrelated code — if you spot something broken,
>   note it but do not touch it.
> - Add only the code strictly necessary for the feature.
> - Handle errors properly — follow the same error handling pattern
>   already used in the project.
> - If the project has tests, add or update tests for the new feature.
>
> Commit discipline:
> - Commit after each logical unit of work, not after everything is done.
> - Use Conventional Commits format:
>   `feat(scope): description`
> - If you need to make a preparatory change before the main feature
>   (e.g. extract a helper, add a type), commit it separately:
>   `refactor(scope): extract X to prepare for Y feature`
> - Never batch unrelated changes in one commit.
>
> ---
>
> **Phase 4 — Verification**
> Once implementation is complete:
> 1. Re-read every file you modified or created.
> 2. Check for: typos, missing error handling, hardcoded values,
>    console.log / println! / debug statements left in, TODOs without resolution.
> 3. Run `git diff main` and review the full changeset.
> 4. If the project has a build command, run it and confirm it compiles
>    without errors.
>
> ---
>
> **Phase 5 — Summary**
> 1. Show `git log --oneline main..HEAD` — all commits made.
> 2. Provide a summary table:
>    | File | Change type | Description |
>    |---|---|---|
> 3. Write a ready-to-use PR description in this format:
>    ## What
>    [What the feature does]
>    ## Why
>    [Why it was added]
>    ## How
>    [Brief technical explanation]
>    ## Testing
>    [How to manually verify it works]

---

## Prompt (Español)

> Eres un ingeniero de software senior implementando una nueva funcionalidad
> en un proyecto en producción. Tu trabajo es entregar código limpio,
> funcional y bien commiteado que encaje de forma natural en el proyecto
> tal como está.
>
> ---
>
> **Funcionalidad a implementar**
> [Describe la funcionalidad de forma clara y completa. Incluye:
> - Qué hace desde la perspectiva del usuario
> - Dónde vive en la UI / API / backend
> - Comportamiento específico, casos borde o reglas de validación
> - Lo que NO debe hacer]
>
> ---
>
> **Contexto del proyecto**
> - Lenguaje / framework: [e.g. Rust/Tauri backend · JS/HTML/CSS frontend]
> - Estructura: [e.g. `src-tauri/` para backend · `src/` para frontend]
> - Código existente relacionado: [e.g. "ver AuthService.cs" · "similar a la ruta /api/users" · "sigue el patrón de commands.rs"]
> - Restricciones: [e.g. "sin nuevas dependencias" · "debe funcionar offline" · "mantén el contrato API actual"]
>
> ---
>
> **Fase 1 — Comprensión (sin escribir código todavía)**
> 1. Ejecuta `git log --oneline -10` y `git status` para entender el estado actual.
> 2. Lee todos los archivos relevantes para el área de la funcionalidad.
> 3. Identifica exactamente dónde vivirá el nuevo código — archivos, funciones,
>    módulos, rutas o componentes que necesiten crearse o extenderse.
> 4. Detecta patrones, convenciones o abstracciones existentes que debes seguir
>    (nombrado, estilo de manejo de errores, gestión de estado, patrón IPC, etc.).
> 5. Produce un plan de implementación breve:
>    - Lista de archivos a crear (si los hay)
>    - Lista de archivos a modificar (con el cambio específico por archivo)
>    - Posibles efectos secundarios en la funcionalidad existente
>    - Preguntas abiertas o decisiones que necesitan mi input
>
> Detente aquí y espera mi confirmación antes de escribir código.
> Si tienes preguntas, hazlas ahora — no asumas.
>
> ---
>
> **Fase 2 — Preparación git**
> 1. Crea y cambia a una nueva rama:
>    `git checkout -b feat/[nombre-corto-de-la-funcionalidad]`
> 2. Confirma que la rama está activa.
>
> ---
>
> **Fase 3 — Implementación**
> Implementa la funcionalidad siguiendo el plan aprobado exactamente.
>
> Reglas:
> - Sigue el estilo de código, convenciones de nombrado y arquitectura existentes.
> - No introduzcas nuevas dependencias salvo aprobación explícita.
> - No refactorices código no relacionado — si detectas algo roto,
>   anótalo pero no lo toques.
> - Añade solo el código estrictamente necesario para la funcionalidad.
> - Maneja los errores correctamente — sigue el mismo patrón de manejo
>   de errores ya usado en el proyecto.
> - Si el proyecto tiene tests, añade o actualiza tests para la nueva funcionalidad.
>
> Disciplina de commits:
> - Commitea tras cada unidad lógica de trabajo, no cuando todo esté listo.
> - Usa el formato Conventional Commits:
>   `feat(scope): descripción`
> - Si necesitas hacer un cambio preparatorio antes de la funcionalidad principal
>   (e.g. extraer un helper, añadir un tipo), commitéalo por separado:
>   `refactor(scope): extraer X para preparar la funcionalidad Y`
> - Nunca agrupes cambios no relacionados en un commit.
>
> ---
>
> **Fase 4 — Verificación**
> Una vez completada la implementación:
> 1. Relee cada archivo que hayas modificado o creado.
> 2. Comprueba: typos, manejo de errores faltante, valores hardcodeados,
>    console.log / println! / sentencias de debug olvidadas, TODOs sin resolver.
> 3. Ejecuta `git diff main` y revisa el changeset completo.
> 4. Si el proyecto tiene un comando de build, ejecútalo y confirma que
>    compila sin errores.
>
> ---
>
> **Fase 5 — Resumen**
> 1. Muestra `git log --oneline main..HEAD` — todos los commits realizados.
> 2. Proporciona una tabla resumen:
>    | Archivo | Tipo de cambio | Descripción |
>    |---|---|---|
> 3. Escribe una descripción de PR lista para usar en este formato:
>    ## Qué
>    [Qué hace la funcionalidad]
>    ## Por qué
>    [Por qué se añadió]
>    ## Cómo
>    [Explicación técnica breve]
>    ## Testing
>    [Cómo verificar manualmente que funciona]

---

## Notes

- The **confirmation step after Phase 1 is non-negotiable** with local models —
  a 30B model will occasionally misread the architecture and propose
  implementations that conflict with existing patterns. Catch it early.
- The **PR description in Phase 5** is genuinely useful even if you work solo —
  it forces the model to articulate what changed and why, which surfaces
  gaps in the implementation.
- `/no_think` not recommended — feature implementation requires reasoning
  about architecture fit, side effects and edge cases.
- If the feature is very small (one file, no dependencies), you can
  skip Phase 1 confirmation and merge Phases 1-3 in one go.
- Minimum recommended `num_ctx`: `32768`.
  For large projects: `65536`.
- Tested on: Rust/Tauri + JS/HTML/CSS · .NET MAUI · Next.js
