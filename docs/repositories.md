# Repositories

## Overview

| Repository | Tech Stack | Deploy Target | Branch Strategy |
|---|---|---|---|
| {{REPO_1_NAME}} | {{TECH_STACK}} | {{DEPLOY_TARGET}} | {{BRANCH_STRATEGY}} |
| {{REPO_2_NAME}} | {{TECH_STACK}} | {{DEPLOY_TARGET}} | {{BRANCH_STRATEGY}} |
| {{REPO_3_NAME}} | {{TECH_STACK}} | {{DEPLOY_TARGET}} | {{BRANCH_STRATEGY}} |

## Relationships

Describe how the repositories relate to each other:

- **{{REPO_1_NAME}}** serves the API consumed by {{REPO_2_NAME}} and {{REPO_3_NAME}}
- **{{REPO_2_NAME}}** and **{{REPO_3_NAME}}** are mobile clients that share the same API

## Repository Setup

Each repository should have its own `CLAUDE.md` at its root with:

1. **Tech stack** — language, framework, major dependencies
2. **Architecture** — directory structure, key modules, data flow
3. **Conventions** — naming, file organization, code style
4. **Key files** — config files, entry points, important modules
5. **Common commands** — build, test, lint, deploy
6. **Gotchas** — known issues, workarounds, non-obvious behaviors
