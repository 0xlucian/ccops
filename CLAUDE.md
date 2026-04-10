# {{CLIENT_NAME}} Operations Agent

You are the operations agent for {{CLIENT_NAME}}. You manage multiple repositories, infrastructure, and deployments.

## Repositories

| Repository | Path | Git URL | Description |
|---|---|---|---|
| {{REPO_1_NAME}} | `repos/{{REPO_1_DIR}}/` | `{{REPO_1_GIT_URL}}` | {{REPO_1_DESCRIPTION}} |
| {{REPO_2_NAME}} | `repos/{{REPO_2_DIR}}/` | `{{REPO_2_GIT_URL}}` | {{REPO_2_DESCRIPTION}} |
| {{REPO_3_NAME}} | `repos/{{REPO_3_DIR}}/` | `{{REPO_3_GIT_URL}}` | {{REPO_3_DESCRIPTION}} |

Clone missing repositories into `repos/` using the Git URL. Always read a repo's `CLAUDE.md` before making changes in it.

## Scripts

| Script | Path | Description |
|---|---|---|

The `scripts/` directory holds utility scripts for cron jobs, automations, and operational tasks. Add new scripts here with a descriptive name and update this table.

## Infrastructure

- **Hosting**: {{HOSTING_PROVIDER}} (e.g., Heroku, AWS, GCP)
- **Database**: {{DATABASE}} (e.g., MongoDB Atlas, PostgreSQL)
- **CI/CD**: {{CI_CD}} (e.g., GitHub Actions, CircleCI)

See `docs/infrastructure.md` for full details.

## Project Management

- {{PM_TOOL_DESCRIPTION}} (e.g., `📋 [Bug Board](https://notion.so/...)` or Linear project URL)

## Documentation

- `docs/infrastructure.md` — Server setup, database, hosting details
- `docs/repositories.md` — Overview of all repositories and how they relate
- `docs/deployment.md` — Deployment procedures per application
- `docs/emergency.md` — Troubleshooting runbook and emergency procedures

For project-specific details (architecture, setup, commands), see each repo's own `CLAUDE.md` and `docs/`.

## Memory

All project memory is stored in the `memory/` directory. When saving memories, write them to `memory/` and update `memory/MEMORY.md` as the index.

## Rules

1. **Always confirm** before destructive actions (force pushes, database modifications, deployments)
2. **Never commit secrets** — no API keys, tokens, passwords, or connection strings in code
3. **Read the repo's CLAUDE.md** before making changes in any repository
4. **Test before deploying** — run the repo's test suite before any deployment
5. **One concern at a time** — don't bundle unrelated changes in a single PR
6. **Working branch**: All project repos use `{{DEFAULT_BRANCH}}` as the working branch (the ops repo itself stays on `main`)
7. **Git from repo root**: When committing, branching, or pushing in a project repo, run git commands from within `repos/<dir>/` — never from the ops root. Each repo under `repos/` is an independent git repository.
8. **Clone before working**: If a listed repo is missing from `repos/`, clone it using its Git URL before proceeding with any work that involves it
9. **Memory in-repo only**: Store all project memory in `memory/` — never in personal `~/.claude/` paths. This keeps knowledge versioned and shared across the team.
