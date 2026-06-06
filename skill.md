---
name: readme-architect
description: Generates, improves, fixes, and updates professional README.md files for software projects. Use this skill whenever the user asks to write, create, generate, improve, fix, or update a README.md. Triggers on phrases like "write a README", "create a README for my project", "generate README", "improve my README", "fix the README", "update README", "add a README", "my README is missing X", or any request involving README documentation for a software project. Always use this skill — don't try to wing a README without it.
metadata:
    version: "1.0.0"
    author: ssant0
---

# README Architect

Your job is to produce a high-quality, professional `README.md` file. Write READMEs in English by default unless the user explicitly asks for another language. Respond to the user in their own language.

## Step 1: Understand the project

Before writing anything, gather context. Scan the project root for these files (read whichever exist):

- `package.json` / `package-lock.json` — Node/frontend projects
- `go.mod` — Go projects
- `pom.xml` / `build.gradle` — Java projects
- `Cargo.toml` — Rust projects
- `pyproject.toml` / `requirements.txt` / `setup.py` — Python projects
- `docker-compose.yml` / `Dockerfile` — containerized or DevOps projects
- `angular.json` / `astro.config.*` / `vite.config.*` — frontend frameworks
- `.github/workflows/` — CI/CD pipelines
- Existing `README.md` — if improving/fixing, read it fully first

If you're missing critical information (project name, purpose, main tech), ask the user before writing.

## Step 2: Identify the project type

Pick the closest match — this shapes which sections to emphasize:

- **Frontend** (Angular, React, Vue, Astro, etc.)
- **Backend** (Go, Spring Boot, Express, FastAPI, etc.)
- **Infrastructure / DevOps** (Docker Compose, Kubernetes, Terraform, CI/CD pipelines)
- **Monorepo** (frontend + backend in the same repo)
- **Library / Package** (published to npm, PyPI, crates.io, etc.)

## Step 3: Build the README

Every README must include these sections in this order:

### 1. Header
- Project title with a relevant emoji
- One-line description of what it does and for whom
- Badges: build status, version, primary language/framework, license

### 2. Description
Two to three sentences. What problem does it solve? Who uses it?

### 3. Table of Contents
Anchor links to all major sections.

### 4. Tech Stack
Bullet list of primary languages, frameworks, and infrastructure tools.

### 5. Prerequisites
Exact versions required (e.g., `Go >= 1.21`, `Node.js >= 20.x`, `Docker >= 24`).

### 6. Installation
Step-by-step from `git clone` to a running app. Use bash code blocks.

### 7. Environment Variables
Table format:

| Variable | Description | Environment | Required |
|---|---|---|---|
| `DB_URL` | PostgreSQL connection string | All | Yes |
| `JWT_SECRET` | Token signing key | Prod | Yes |

Include instructions to copy `.env.example` if it exists.

### 8. Usage / Development
Commands to start the dev environment. Separate dev from prod commands.

### 9. Available Scripts
What each command in `Makefile`, `package.json scripts`, or `justfile` does.

### 10. Contributing
Branch naming convention, commit style (Conventional Commits if applicable), PR process.

### 11. License
State the license type.

---

## Project-type additions

Layer these on top of the standard structure based on what you detected in Step 2:

### Frontend projects
- Rendering mode: SSR, SSG, or CSR
- State management approach
- Build commands: dev vs. production
- Lighthouse / performance notes if relevant

### Backend projects
- Architecture pattern (Hexagonal, Clean, MVC, etc.)
- Database migration instructions
- API documentation link (Swagger/OpenAPI/Postman collection)
- How to run the test suite

### Infrastructure / DevOps projects
- Network topology: which ports are exposed, how containers communicate
- CI/CD pipeline explanation (what triggers what)
- How secrets are injected in production
- Backup/restore strategy for data volumes

### Monorepos
- Workspace structure (how frontend and backend are split)
- How to start the full stack locally (e.g., `docker-compose` + parallel scripts)

### Libraries / Packages
- Installation via package manager (`npm install`, `go get`, `pip install`)
- Quick-start code example showing the most common use case
- Full API reference or link to docs site

---

## Formatting rules

- Use GitHub Flavored Markdown (GFM)
- Specify the language on every code block (`bash`, `go`, `ts`, `json`, `yaml`)
- Use GitHub callouts for important warnings:

```
> [!WARNING]
> Never commit `.env` to version control.

> [!IMPORTANT]
> Requires CGO enabled for certain dependencies.

> [!NOTE]
> Compatible with Hyprland and AeroSpace window managers.
```

- Keep badge URLs functional — use shields.io format
- Anchor links in the Table of Contents must match actual heading text

---

## Step 4: Write and save the file

Write the completed README to `README.md` in the project root (or wherever the user specifies). If you're improving or fixing an existing README, make targeted edits rather than rewriting sections that are already good.

After saving, tell the user what you added or changed and why, in 2–3 sentences.
