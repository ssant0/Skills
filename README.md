# 📐 readme-architect

> An AI coding agent skill that generates, improves, and fixes professional `README.md` files for any software project.

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Skill](https://img.shields.io/badge/AI%20Coding%20Agent-Skill-blueviolet)
![License](https://img.shields.io/badge/license-MIT-green)

## Description

`readme-architect` is a skill for AI coding agents that produces high-quality, structured `README.md` files from project context alone. It detects your stack, selects the right sections for your project type, and writes in GitHub Flavored Markdown — so you get a README worth reading without writing a single line yourself.

## Table of Contents

- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [Supported Project Types](#supported-project-types)
- [Contributing](#contributing)
- [License](#license)

## Tech Stack

- **AI Coding Agent Skills** — skill runtime
- **Markdown (GFM)** — output format
- **shields.io** — badge generation

## Installation

```bash
npx skills add ssant0/readme-architect
```

Once installed, the skill is available in any compatible AI coding agent session.

## Usage

Trigger the skill with natural language inside Claude Code:

```
write a README for this project
create a README for my API
generate README
improve my README
fix the README
update the README — add a section about environment variables
my README is missing the installation steps
```

The skill detects your intent and runs automatically — no slash command needed.

## How It Works

1. **Scans the project root** for `package.json`, `go.mod`, `Cargo.toml`, `pyproject.toml`, `docker-compose.yml`, `Dockerfile`, framework config files, and CI/CD workflows.
2. **Identifies the project type** (Frontend, Backend, Infrastructure, Monorepo, or Library/Package).
3. **Builds the README** with the standard section set, then layers in project-type-specific sections on top.
4. **Writes the file** to `README.md` in the project root (or wherever you specify).

When improving an existing README, it makes targeted edits instead of rewriting sections that are already good.

## Supported Project Types

| Type | Extra sections added |
| --- | --- |
| **Frontend** | Rendering mode, state management, build commands, Lighthouse notes |
| **Backend** | Architecture pattern, migrations, API docs link, test suite |
| **Infrastructure / DevOps** | Network topology, CI/CD explanation, secrets strategy, backup/restore |
| **Monorepo** | Workspace structure, full-stack local startup |
| **Library / Package** | Package manager install, quick-start example, API reference |

## Contributing

Branch naming: `feat/<topic>`, `fix/<topic>`, `docs/<topic>`

Commits follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(skill): add Rust project detection
fix(formatting): correct badge URL template
docs(readme): update usage examples
```

Open a PR against `main`. Include the trigger phrases you tested in the PR description.

## License

MIT
