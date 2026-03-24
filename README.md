# ccops — Claude Code Operations Template

A template repository for setting up a Claude Code operations agent that manages multiple repositories, infrastructure, and deployments.

## Quick Start

### 1. Fork this repository

Fork `ccops` to create your client-specific ops repo (e.g., `acme-ops`).

### 2. Configure

Replace all `{{PLACEHOLDER}}` values in:
- `CLAUDE.md` — Agent identity, repository table, infrastructure details
- `docs/*.md` — Infrastructure, deployment, and database documentation
- Each repo's `CLAUDE.md` (created in step 4)

### 3. Add skills

Place skills in `.claude/skills/`. See `.claude/skills/SKILL.md` for the template and conventions.

Skills added here are available to:
- The nairid agent running on the server (automatic)
- Local Claude Code users who run from this repo's root directory

### 4. Deploy the agent

On the server:

```bash
# Clone your forked ops repo
git clone git@github.com:your-org/acme-ops.git
cd acme-ops

# Clone managed repositories into repos/
git clone git@github.com:your-org/backend.git repos/backend
git clone git@github.com:your-org/mobile-ios.git repos/mobile-ios
git clone git@github.com:your-org/mobile-android.git repos/mobile-android

# Add CLAUDE.md to each repo if not already present
# Deploy nairid agent with this directory as working directory
```

### 5. Local development

Developers can clone the forked ops repo and run Claude Code from the root:

```bash
git clone git@github.com:your-org/acme-ops.git
cd acme-ops
git clone git@github.com:your-org/backend.git repos/backend
# Run Claude Code from here — skills and root context are available
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
│   ├── db.md                   # Database schema and queries
│   └── emergency.md            # Troubleshooting runbook
├── .claude/
│   └── skills/                 # Agent skills (portable)
│       └── SKILL.md            # Skill conventions and template
├── memory/                     # Agent learnings (git-tracked)
│   └── .gitkeep
└── repos/                      # Git-ignored, cloned at runtime
    ├── backend/
    ├── mobile-ios/
    └── mobile-android/
```

## Key Principles

- **Root CLAUDE.md stays thin** — high-level identity, repo table, pointers to docs. Each repo has its own CLAUDE.md with detailed context.
- **Skills live here** — ops-level skills belong in the ops repo, not in individual project repos.
- **repos/ is runtime-only** — never committed, cloned on each environment (server or local dev).
- **memory/ is git-tracked** — agent learnings persist across redeployments.
