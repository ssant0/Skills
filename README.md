# 🧰 Skills

> A monorepo of utility skills for AI coding agents (Claude Code and compatible agents) — each one solves a specific problem during the coding workflow.

![Skills](https://img.shields.io/badge/AI%20Coding%20Agent-Skills-blueviolet)
![License](https://img.shields.io/badge/license-MIT-green)

## Description

This repository is a collection of independent, installable **skills** for AI coding agents. Each skill lives in its own folder, targets one specific problem (architecture questions before coding, README generation, etc.), and ships with its own `SKILL.md`/`skill.md` definition, `README.md`, and `LICENSE`. This root README is just the index: a map of what's available and how to install it. For details on any individual skill, follow its link below — each one is fully documented on its own.

## Table of Contents

- [Available Skills](#available-skills)
- [Repository Structure](#repository-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Adding a New Skill](#adding-a-new-skill)
- [Contributing](#contributing)
- [License](#license)

## Available Skills

| Skill | Description |
| --- | --- |
| [**d2cp-router**](./d2cp-router/README.md) | Acts as a Software Architect before writing code — detects missing context or ambiguity in a request and asks targeted questions (with concrete options) before any implementation begins, using the D2CP cycle (Decision, Direction, Criterion, Precision). |
| [**readme-architect**](./readme-architect/README.md) | Generates, improves, fixes, and updates professional `README.md` files for software projects, adapting the structure to the project type (frontend, backend, infra, monorepo, library). |

> [!NOTE]
> Each skill folder is self-contained: it has its own `README.md` with installation, usage, and behavior details, plus its own `LICENSE`. This table is kept up to date whenever a new skill is added to the repo.

## Repository Structure

```text
Skills/
├── README.md              # This file — index of all skills
├── d2cp-router/
│   ├── SKILL.md            # Skill definition (trigger + instructions)
│   ├── README.md           # Skill-specific documentation
│   └── LICENSE
└── readme-architect/
    ├── skill.md             # Skill definition (trigger + instructions)
    ├── README.md           # Skill-specific documentation
    └── LICENSE
```

## Installation

Skills are installed individually using the [`skills` CLI](https://www.npmjs.com/package/skills):

```bash
npx skills add ssant0/Skills --skill <skill-name>
```

For example:

```bash
npx skills add ssant0/Skills --skill d2cp-router
npx skills add ssant0/Skills --skill readme-architect
```

Once installed, each skill activates automatically in any compatible AI coding agent session — no manual configuration or slash commands required.

## Usage

Each skill triggers on natural-language requests relevant to its purpose:

- **d2cp-router** activates when you ask the agent to start a new project, build a feature, or make architectural decisions (e.g., "build a login", "set up a backend", "add payments").
- **readme-architect** activates when you ask the agent to write, generate, improve, or fix a `README.md`.

See each skill's own README (linked in the table above) for full trigger phrases and behavior.

## Adding a New Skill

1. Create a new top-level folder named after the skill (kebab-case).
2. Add the skill definition file (`SKILL.md` or `skill.md`) with frontmatter (`name`, `description`, `metadata`).
3. Add a skill-specific `README.md` following the structure produced by `readme-architect`.
4. Add a `LICENSE` file for the skill.
5. Add a row for the new skill in the [Available Skills](#available-skills) table in this file.

## Contributing

Branch naming: `feat/<skill-name>`, `fix/<skill-name>`, `docs/<skill-name>`

Commits follow [Conventional Commits](https://www.conventionalcommits.org/):

```text
feat(skill-name): add new skill
fix(skill-name): correct trigger description
docs(readme): update skills catalog
```

Open a PR against `main`. If you're adding a new skill, make sure the root [Available Skills](#available-skills) table is updated.

## License

Each skill is individually licensed under MIT — see the `LICENSE` file inside its folder.
