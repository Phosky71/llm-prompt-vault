---
title: "Refactor a specific module or file"
tool: claude-code
backend: ollama
model: qwen3-coder:30b
tags: [refactor, clean-code, structure, git]
tested: false
no_think: not recommended
---

# Refactor a Specific Module

Use this to improve the internal structure, readability or maintainability
of a specific part of the codebase without changing its external behavior.

Best for: files that have grown too large, functions doing too many things,
duplicated logic, inconsistent error handling, hard-to-follow control flow.

**Scope this to one file or module at a time. Never refactor the whole
project in one shot — especially with a local model.**

---

## Prompt (English)

> You are a senior software engineer performing a scoped, disciplined
> refactor. Your job is to improve the internal quality of a specific
> part of the codebase without changing its observable behavior.
> Every external interface, method signature and public contract
> must remain exactly the same after your changes.
>
> ---
>
> **Refactor target**
> - File(s) / module(s): [e.g. `src-tauri/src/commands.rs` · `src/services/AuthService.cs`]
> - Reason for refactoring: [e.g. "function is 300 lines long" · "logic is duplicated in 3 places" · "error handling is inconsistent"]
> - Known constraints: [e.g. "public API must stay the same" · "no new dependencies" · "must stay compatible with X"]
>
> ---
>
> **Phase 1 — Analysis (do not modify anything yet)**
> 1. Run `git status` to confirm the working tree is clean before starting.
>    If there are uncommitted changes, stop and tell me — do not proceed.
> 2. Read the target file(s) completely.
> 3. Read any files that depend on or are imported by the target
>    to understand the full impact radius of changes.
> 4. Produce a refactor plan:
>    - List every specific change you intend to make
>      (e.g. "extract lines 45-78 into a `validate_input()` function")
>    - For each change, explain why it improves the code
>    - Confirm explicitly which parts you will NOT touch
>    - Flag any change that could have side effects, even minor ones
>
> Stop here and wait for my confirmation before making any change.
> If any planned change feels risky or uncertain, flag it explicitly.
>
> ---
>
> **Phase 2 — Git setup**
> 1. Create and switch to a new branch:
>    `git checkout -b refactor/[short-module-name]`
> 2. Confirm the branch is active.
>
> ---
>
> **Phase 3 — Refactor**
> Apply the approved changes following these rules:
>
> Non-negotiable rules:
> - Do NOT change any public method signature, return type or interface.
> - Do NOT change observable behavior — same input must produce same output.
> - Do NOT touch files outside the agreed scope.
> - Do NOT introduce new dependencies.
> - Do NOT fix bugs you find along the way — note them, do not touch them.
>   Bug fixes belong in `debug/fix-errors.md`, not here.
>
> Code quality rules:
> - Apply the same naming conventions already used in the project.
> - Keep the same error handling style — do not switch paradigms
>   (e.g. do not replace Result<> with exceptions or vice versa).
> - If you extract a function or method, place it logically —
>   private helpers near their caller, shared utils in the right module.
> - Remove dead code only if you are 100% certain it is unreachable.
>
> Commit discipline:
> - One commit per logical refactor unit.
>   Example sequence:
>   `refactor(commands): extract validate_repository_path into helper`
>   `refactor(commands): simplify add_repository control flow`
>   `refactor(commands): remove duplicated error mapping logic`
> - Never batch all changes into a single commit.
> - Use format: `refactor(scope): description`
>
> ---
>
> **Phase 4 — Verification**
> Once all changes are applied:
> 1. Re-read the refactored file(s) from top to bottom.
> 2. Verify:
>    - All public interfaces are identical to before
>    - No debug statements, TODOs without resolution or commented-out code left in
>    - No hardcoded values introduced
>    - Imports are clean — no unused imports added or left behind
> 3. Run `git diff main` and do a final review of the full changeset.
> 4. If the project has a build command, run it. Confirm zero errors.
> 5. If the project has tests, run them. All existing tests must still pass.
>
> ---
>
> **Phase 5 — Summary**
> 1. Show `git log --oneline main..HEAD`.
> 2. Provide a before/after summary for each significant change:
>    | Change | Before | After | Why |
>    |---|---|---|---|
> 3. List any bugs or issues spotted during refactor that were intentionally
>    left untouched — these should go into `debug/fix-errors.md` next.

---

## Prompt (Español)

> Eres un ingeniero de software senior realizando un refactor acotado
> y disciplinado. Tu trabajo es mejorar la calidad interna de una parte
> específica del código sin cambiar su comportamiento observable.
> Cada interfaz externa, firma de método y contrato público debe
> permanecer exactamente igual tras tus cambios.
>
> ---
>
> **Objetivo del refactor**
> - Archivo(s) / módulo(s): [e.g. `src-tauri/src/commands.rs` · `src/services/AuthService.cs`]
> - Motivo del refactor: [e.g. "la función tiene 300 líneas" · "la lógica está duplicada en 3 sitios" · "el manejo de errores es inconsistente"]
> - Restricciones conocidas: [e.g. "la API pública debe mantenerse igual" · "sin nuevas dependencias" · "debe seguir siendo compatible con X"]
>
> ---
>
> **Fase 1 — Análisis (sin modificar nada todavía)**
> 1. Ejecuta `git status` para confirmar que el árbol de trabajo está limpio.
>    Si hay cambios sin commitear, detente y dímelo — no procedas.
> 2. Lee el archivo objetivo completamente.
> 3. Lee los archivos que dependan del objetivo o que este importe,
>    para entender el radio de impacto completo de los cambios.
> 4. Produce un plan de refactor:
>    - Lista cada cambio específico que vas a hacer
>      (e.g. "extraer líneas 45-78 a una función `validate_input()`")
>    - Por cada cambio, explica por qué mejora el código
>    - Confirma explícitamente qué partes NO vas a tocar
>    - Señala cualquier cambio que pueda tener efectos secundarios, aunque sean menores
>
> Detente aquí y espera mi confirmación antes de hacer ningún cambio.
> Si algún cambio planificado te parece arriesgado o incierto, señálalo explícitamente.
>
> ---
>
> **Fase 2 — Preparación git**
> 1. Crea y cambia a una nueva rama:
>    `git checkout -b refactor/[nombre-corto-del-modulo]`
> 2. Confirma que la rama está activa.
>
> ---
>
> **Fase 3 — Refactor**
> Aplica los cambios aprobados siguiendo estas reglas:
>
> Reglas no negociables:
> - NO cambies ninguna firma de método público, tipo de retorno o interfaz.
> - NO cambies el comportamiento observable — el mismo input debe producir el mismo output.
> - NO toques archivos fuera del alcance acordado.
> - NO introduzcas nuevas dependencias.
> - NO arregles bugs que encuentres por el camino — anótalos, no los toques.
>   Los arreglos de bugs pertenecen a `debug/fix-errors.md`, no aquí.
>
> Reglas de calidad de código:
> - Aplica las mismas convenciones de nombrado ya usadas en el proyecto.
> - Mantén el mismo estilo de manejo de errores — no cambies de paradigma
>   (e.g. no sustituyas Result<> por excepciones ni viceversa).
> - Si extraes una función o método, colócalo lógicamente —
>   helpers privados cerca de su caller, utils compartidas en el módulo correcto.
> - Elimina código muerto solo si estás 100% seguro de que es inalcanzable.
>
> Disciplina de commits:
> - Un commit por unidad lógica de refactor.
>   Ejemplo de secuencia:
>   `refactor(commands): extraer validate_repository_path a helper`
>   `refactor(commands): simplificar flujo de control de add_repository`
>   `refactor(commands): eliminar lógica duplicada de error mapping`
> - Nunca agrupes todos los cambios en un solo commit.
> - Formato: `refactor(scope): descripción`
>
> ---
>
> **Fase 4 — Verificación**
> Una vez aplicados todos los cambios:
> 1. Relee el archivo refactorizado de principio a fin.
> 2. Verifica:
>    - Todas las interfaces públicas son idénticas a antes
>    - Sin sentencias de debug, TODOs sin resolver ni código comentado
>    - Sin valores hardcodeados introducidos
>    - Imports limpios — sin imports sin usar añadidos ni dejados atrás
> 3. Ejecuta `git diff main` y haz una revisión final del changeset completo.
> 4. Si el proyecto tiene un comando de build, ejecútalo. Confirma cero errores.
> 5. Si el proyecto tiene tests, ejecútalos. Todos los tests existentes deben seguir pasando.
>
> ---
>
> **Fase 5 — Resumen**
> 1. Muestra `git log --oneline main..HEAD`.
> 2. Proporciona un resumen antes/después para cada cambio significativo:
>    | Cambio | Antes | Después | Por qué |
>    |---|---|---|---|
> 3. Lista bugs o problemas detectados durante el refactor que se dejaron
>    intencionalmente sin tocar — estos deberían ir a `debug/fix-errors.md` a continuación.

---

## Notes

- The **`git status` check at the start of Phase 1** is critical — you never
  want to start a refactor on a dirty working tree. Makes rollback much harder.
- The rule **"do not fix bugs during a refactor"** is one of the most
  important in this prompt. Mixing refactor and bug fixes in the same
  branch makes code review and git history unreadable. Use
  `debug/fix-errors.md` after this is merged.
- The **before/after table in Phase 5** is particularly useful for code review —
  it forces the model to articulate the improvement, not just make changes.
- `/no_think` not recommended — the model needs to reason carefully about
  impact radius and side effects before touching anything.
- Minimum recommended `num_ctx`: `32768`.
- Tested on: Rust/Tauri · .NET MAUI · Next.js
