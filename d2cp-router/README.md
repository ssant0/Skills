# 🧭 d2cp-router

> An AI coding agent skill that acts as a Software Architect before writing code — detecting missing context or ambiguity in a request and asking the right questions, with concrete options, before any implementation begins.

![Skill](https://img.shields.io/badge/AI%20Coding%20Agent-Skill-blueviolet)
![License](https://img.shields.io/badge/license-MIT-green)

## Description

`d2cp-router` stops AI coding agents from guessing on ambiguous requests. When a user asks for a new project, a new feature, or a significant change, the skill evaluates the request against four pillars — **D**ecision, **D**irection, **C**riterion, **P**recision (D2CP) — and asks 1-2 targeted questions with concrete options whenever something important is left undefined. The goal is to avoid throwaway work: a wrong stack, a flow that doesn't fit the existing system, or a design that misses an edge case the user already knew about.

## Table of Contents

- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [The D2CP Cycle](#the-d2cp-cycle)
- [When It Applies (and When It Doesn't)](#when-it-applies-and-when-it-doesnt)
- [Contributing](#contributing)
- [License](#license)

## Tech Stack

- **AI Coding Agent Skills** — skill runtime (Claude Code and compatible agents)
- **Markdown** — skill definition format
- **AskUserQuestion** (Claude Code) or equivalent — interactive question tool used to present options

## Installation

```bash
npx skills add ssant0/Skills --skill d2cp-router
```

Once installed, the skill is active in any compatible AI coding agent session and is invoked automatically — no slash command needed.

## Usage

The skill triggers on requests that involve starting something new or making architectural decisions, for example:

```
haz un login
construye una landing page
monta un backend
crea una API
agrega pagos
```

Instead of generating code immediately, the agent first reviews the project (stack, structure, existing conventions) and then asks targeted questions about whatever can't be deduced from the codebase — stack choice, design pattern, database engine, deployment strategy, security trade-offs, or edge-case behavior.

Trivial fixes (typos, a clear one-off bug, a rename) and requests that are already fully specified bypass the skill entirely — the agent just does the work.

## How It Works

1. **Reviews the project once.** Runs `tree -L 3` (or an equivalent `find`) to see the architecture at a glance, then reads only the files needed to understand the stack — `package.json`, `pom.xml`, `go.mod`, main config, the module being touched. It remembers this for the rest of the session and only re-explores if something changes.
2. **Detects entropy.** If the request has several reasonable interpretations that would lead to very different results, the skill flags it. If there's only one sensible interpretation, it proceeds without asking.
3. **Asks concrete questions.** For each open decision, it presents 2-4 numbered/selectable options with a short explanation each, marks a recommended option with "(Recommended)" when applicable, and always leaves room for a custom answer. It waits for the user's response before writing any code.
4. **Summarizes before implementing.** Once questions are answered, it recaps the decisions (stack, flow, scope) in a few lines so the user can correct a misunderstanding before it becomes code.

## The D2CP Cycle

Before generating any code, the agent evaluates the request against these four pillars:

| Pillar | Question it answers | Example |
| --- | --- | --- |
| **Decisión** (Architecture) | Is the stack, design pattern, and end goal clear? | "Does this go in the Go backend or the Angular frontend?" |
| **Dirección** (Flow) | Is the step-by-step logical flow clear? | "Do we build the database connection first or the endpoint?" |
| **Criterio** (Security / Performance) | Are there obvious bottlenecks or vulnerabilities in the request? | Warns *before* writing code if asked to store passwords in plain text. |
| **Precisión** (Edge cases) | What are the exact expected inputs/outputs? | "What happens if the query fails, the data is empty, or the external service doesn't respond?" |

## When It Applies (and When It Doesn't)

| Applies | Doesn't apply |
| --- | --- |
| New projects (web, API, CLI, scripts, infrastructure) | Trivial fixes (typos, a clear single bug, renaming) |
| New features ("add a login", "add payments", "build a landing page") | Tasks where the user already specified everything needed |
| Medium-to-large changes to existing code | Read/explanation questions that don't generate code |
| Critical architecture decisions (stack, design pattern, DB engine, deployment strategy) | |

General rule: if there's **entropy** (several reasonable interpretations with very different outcomes), ask. If there's only one sensible interpretation, work.

## Contributing

Branch naming: `feat/<topic>`, `fix/<topic>`, `docs/<topic>`

Commits follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(router): add new entropy heuristic
fix(questions): correct option ordering
docs(readme): clarify D2CP cycle table
```

Open a PR against `main`. Include example prompts you tested (and the questions the skill asked) in the PR description.

## License

MIT
