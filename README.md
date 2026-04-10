# ccops — Claude Code Operations Template

A template repository for setting up a Claude Code operations agent that manages multiple repositories, infrastructure, and deployments.

## Quick Start

### 1. Fork this repository

Fork `ccops` to create your client-specific ops repo (e.g., `acme-ops`).

### 2. Configure

Run the setup wizard from the repo root:

```bash
claude
# then type: /init
```

The `/init` skill walks you through everything interactively:
- Project name and default branch
- Repositories — clones them and generates per-repo `CLAUDE.md` files
- Architecture overview across all repos
- Project management tool and board link

You can re-run `/init` anytime to fill in items you skipped.

### 3. Add skills

Place skills in `.claude/skills/`. Skills added here are available to:
- The nairid agent running on the server (automatic)
- Local Claude Code users who run from this repo's root directory

### 4. Deploy

On the server:

```bash
# Clone your forked ops repo
git clone git@github.com:your-org/acme-ops.git
cd acme-ops

# Deploy nairid agent with this directory as working directory
# The agent will clone all repositories listed in CLAUDE.md into repos/ on first run
```

### 5. Local development

Developers clone the forked ops repo and run Claude Code from the root:

```bash
git clone git@github.com:your-org/acme-ops.git
cd acme-ops
# Run Claude Code from here — skills and root context are available
# The agent will clone repos as needed based on CLAUDE.md
```

## Structure

```
ccops/
├── CLAUDE.md                   # Root agent prompt (high-level)
├── .gitignore                  # Ignores repos/, secrets, etc.
├── README.md                   # This file
├── docs/                       # Operational documentation
│   ├── infrastructure.md       # Hosting, database, server details
│   ├── repositories.md         # Repo overview and relationships
│   ├── deployment.md           # Deploy procedures per app
│   └── emergency.md            # Troubleshooting runbook
├── scripts/                    # Utility scripts, cron jobs, automations
├── memory/                     # Agent memory (versioned, shared)
│   └── MEMORY.md               # Memory index
├── .claude/
│   └── skills/                 # Agent skills (portable)
└── repos/                      # Git-ignored, cloned at runtime
```

## Key Principles

- **Root CLAUDE.md stays thin** — high-level identity, repo table, pointers to docs. Each repo has its own CLAUDE.md with detailed context.
- **Skills live here** — ops-level skills belong in the ops repo, not in individual project repos.
- **repos/ is runtime-only** — never committed, cloned by the agent on first run.
- **Agent self-bootstraps** — repos listed in CLAUDE.md with git URLs are cloned automatically when missing.
- **Memory lives in-repo** — all agent memory goes in `memory/`, never in `~/.claude/`. This keeps knowledge versioned and shared across the team.
