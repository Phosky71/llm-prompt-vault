---
title: "Generate README for a project"
tool: claude-code
backend: ollama
model: qwen3-coder:30b
tags: [docs, readme, documentation, markdown]
tested: false
no_think: recommended
---

# Generate Project README

Use this to generate a complete, professional README.md based entirely
on the actual code — not assumptions. Claude Code will read the project
first and then write documentation that reflects reality.

Best for: projects with no README, outdated README, or a placeholder
README that needs to be replaced with something real.

---

## Prompt (English)

> You are a technical writer with deep software engineering knowledge.
> Your job is to generate a complete, professional README.md for this
> project based entirely on what you find in the code.
> Do not invent features, steps or details that are not in the codebase.
>
> ---
>
> **Goal**
> Produce a README.md that a developer who has never seen this project
> can use to understand what it does, set it up locally and start
> contributing — without needing to ask anyone anything.
>
> ---
>
> **Phase 1 — Project read**
> Before writing a single line, read and understand:
> 1. Entry point(s) — `main.rs`, `Program.cs`, `index.js`, `app.py`, etc.
> 2. Configuration files — `package.json`, `Cargo.toml`, `.csproj`,
>    `tauri.conf.json`, `.env.example`, `docker-compose.yml`, etc.
> 3. Dependency list — extract the actual tech stack and versions.
> 4. Build and run scripts — what commands are needed to install, build and run.
> 5. Project structure — top-level folders and what each one contains.
> 6. Core features — what the application actually does, derived from the code.
> 7. Existing README if present — use it as a reference but do not copy it
>    blindly. Update and correct anything that is wrong or missing.
>
> If anything is genuinely unclear after reading (e.g. missing .env.example,
> undocumented setup step), flag it as a `> ⚠️ TODO:` block in the README
> rather than inventing a value.
>
> ---
>
> **Phase 2 — Write the README**
> Generate the complete `README.md` using this exact structure:
>
> ```markdown
> # Project Name
>
> > One-sentence description of what this project does.
>
> ![tech badge] ![license badge]  ← only if info is available in the project
>
> ## Features
> - Bullet list of actual features found in the code
> - Be specific — "Add and manage Git repositories" not "Manage data"
>
> ## Tech Stack
> | Layer | Technology | Version |
> |---|---|---|
>
> ## Prerequisites
> List everything needed before installation:
> - Runtime versions (Node.js x, Rust x, .NET x)
> - Required tools (cargo, npm, tauri-cli, etc.)
> - Environment variables needed (reference .env.example if it exists)
>
> ## Installation
> Step-by-step, copy-pasteable commands. No ambiguity.
>
> ```bash
> # clone
> git clone https://github.com/[user]/[repo].git
> cd [repo]
>
> # install dependencies
> [actual commands]
>
> # environment setup
> [actual commands or ⚠️ TODO if unclear]
> ```
>
> ## Running the project
>
> ### Development
> ```bash
> [actual dev command]
> ```
>
> ### Production build
> ```bash
> [actual build command]
> ```
>
> ## Project Structure
> ```
> [directory tree — top 2 levels, with a one-line comment per folder]
> ```
>
> ## Configuration
> Explain any configuration files or environment variables.
> Reference the actual keys found in the project.
>
> ## Contributing
> ```bash
> git checkout -b feat/your-feature
> # make changes
> git commit -m "feat(scope): description"
> git push origin feat/your-feature
> # open a Pull Request
> ```
>
> ## License
> [License type found in LICENSE file, or ⚠️ TODO: add LICENSE file]
> ```
>
> ---
>
> **Phase 3 — Write to disk**
> 1. If a README.md already exists, overwrite it.
> 2. Commit the result:
>    `git add README.md`
>    `git commit -m "docs: generate complete README from codebase"`
>
> ---
>
> **Rules**
> - Every installation step must be real and tested against the actual
>   project files — do not copy generic steps from memory.
> - Use `> ⚠️ TODO: [explain what is missing]` for anything you cannot
>   determine from the code. Never invent values.
> - Keep the tone technical but approachable. No marketing language.
> - English only, unless the project is explicitly in another language.
> - Do not add sections not listed above unless the project genuinely
>   needs them (e.g. API reference for a library, screenshots for a GUI app).

---

## Prompt (Español)

> Eres un escritor técnico con profundo conocimiento de ingeniería de software.
> Tu trabajo es generar un README.md completo y profesional para este proyecto
> basándote exclusivamente en lo que encuentres en el código.
> No inventes funcionalidades, pasos ni detalles que no estén en el código.
>
> ---
>
> **Objetivo**
> Producir un README.md que un desarrollador que nunca ha visto este proyecto
> pueda usar para entender qué hace, configurarlo en local y empezar a
> contribuir — sin necesidad de preguntarle nada a nadie.
>
> ---
>
> **Fase 1 — Lectura del proyecto**
> Antes de escribir una sola línea, lee y comprende:
> 1. Punto(s) de entrada — `main.rs`, `Program.cs`, `index.js`, `app.py`, etc.
> 2. Archivos de configuración — `package.json`, `Cargo.toml`, `.csproj`,
>    `tauri.conf.json`, `.env.example`, `docker-compose.yml`, etc.
> 3. Lista de dependencias — extrae el stack tecnológico real y versiones.
> 4. Scripts de build y ejecución — qué comandos se necesitan para instalar,
>    compilar y ejecutar.
> 5. Estructura del proyecto — carpetas de primer nivel y qué contiene cada una.
> 6. Funcionalidades principales — qué hace realmente la aplicación, derivado del código.
> 7. README existente si lo hay — úsalo como referencia pero no lo copies
>    ciegamente. Actualiza y corrige lo que esté mal o incompleto.
>
> Si algo no está claro tras la lectura (e.g. falta .env.example, paso de
> configuración no documentado), márcalo como `> ⚠️ TODO:` en el README
> en lugar de inventar un valor.
>
> ---
>
> **Fase 2 — Escribir el README**
> Genera el `README.md` completo usando exactamente esta estructura:
>
> ```markdown
> # Nombre del proyecto
>
> > Descripción en una frase de qué hace este proyecto.
>
> ![badge tech] ![badge licencia]  ← solo si la info está disponible en el proyecto
>
> ## Funcionalidades
> - Lista de funcionalidades reales encontradas en el código
> - Sé específico — "Añadir y gestionar repositorios Git" no "Gestionar datos"
>
> ## Stack tecnológico
> | Capa | Tecnología | Versión |
> |---|---|---|
>
> ## Requisitos previos
> Lista todo lo necesario antes de la instalación:
> - Versiones de runtime (Node.js x, Rust x, .NET x)
> - Herramientas requeridas (cargo, npm, tauri-cli, etc.)
> - Variables de entorno necesarias (referencia a .env.example si existe)
>
> ## Instalación
> Pasos copiables y sin ambigüedad.
>
> ```bash
> # clonar
> git clone https://github.com/[user]/[repo].git
> cd [repo]
>
> # instalar dependencias
> [comandos reales]
>
> # configuración del entorno
> [comandos reales o ⚠️ TODO si no está claro]
> ```
>
> ## Ejecutar el proyecto
>
> ### Desarrollo
> ```bash
> [comando real de desarrollo]
> ```
>
> ### Build de producción
> ```bash
> [comando real de build]
> ```
>
> ## Estructura del proyecto
> ```
> [árbol de directorios — 2 niveles, con comentario de una línea por carpeta]
> ```
>
> ## Configuración
> Explica los archivos de configuración o variables de entorno.
> Referencia las claves reales encontradas en el proyecto.
>
> ## Contribuir
> ```bash
> git checkout -b feat/tu-funcionalidad
> # realizar cambios
> git commit -m "feat(scope): descripción"
> git push origin feat/tu-funcionalidad
> # abrir un Pull Request
> ```
>
> ## Licencia
> [Tipo de licencia del archivo LICENSE, o ⚠️ TODO: añadir archivo LICENSE]
> ```
>
> ---
>
> **Fase 3 — Escribir en disco**
> 1. Si ya existe un README.md, sobreescríbelo.
> 2. Commitea el resultado:
>    `git add README.md`
>    `git commit -m "docs: generar README completo desde el código"`
>
> ---
>
> **Reglas**
> - Cada paso de instalación debe ser real y contrastado con los archivos
>   reales del proyecto — no copies pasos genéricos de memoria.
> - Usa `> ⚠️ TODO: [explica qué falta]` para todo lo que no puedas
>   determinar del código. Nunca inventes valores.
> - Tono técnico pero accesible. Sin lenguaje de marketing.
> - En español si el proyecto está en español, inglés en caso contrario.
> - No añadas secciones no listadas salvo que el proyecto las necesite
>   genuinamente (e.g. referencia de API para una librería, capturas para una app GUI).

---

## Notes

- The **`⚠️ TODO` convention** is the most important rule here — a README
  with honest gaps is infinitely more useful than one with invented steps
  that silently fail when someone follows them.
- `/no_think` recommended — this is a structured writing task. Deep
  reasoning is not needed and only slows down generation.
- If the project has a GUI (like Tauri), prompt Claude Code to also
  note that screenshots can be added manually to a `/docs/screenshots/`
  folder — the model cannot take screenshots.
- Run this after `full-project-review.md` if you want the README to
  also reflect known issues or limitations.
- Minimum recommended `num_ctx`: `32768`.
- Tested on: Rust/Tauri + JS/HTML/CSS · .NET MAUI · Next.js
