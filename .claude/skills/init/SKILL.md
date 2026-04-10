---
name: init
description: >
  Interactive setup wizard for new ccops instances. Walks the user through configuring repositories,
  cloning them, generating per-repo CLAUDE.md files, building an architecture overview, and setting up
  project management. Run after forking the ccops template to bootstrap the entire ops structure.
  Use when the user says "init", "set up this template", "configure this project", "onboard a new project",
  or any variation of initializing a freshly forked ccops repo.
user_invocable: true
---

# Init — ccops Setup Wizard

Bootstrap a freshly forked ccops template into a fully configured operations repo. The wizard is conversational — ask one thing at a time, confirm before moving on.

## Before Starting

Scan all `.md` files in the repo root and `docs/` for remaining `{{...}}` placeholders. If none are found and repos are already cloned, tell the user the project looks fully configured and ask what they'd like to update.

If some sections are already filled in (partial setup), skip those — only ask about what's left. This means `/init` can be re-run to fill in gaps or `TODO` items from a previous run.

## Setup Flow

### Step 1: Project Identity

Ask:
- What is the project/client name? → replaces `{{CLIENT_NAME}}`
- What is the default working branch across repos? (e.g., `main`, `dev`) → replaces `{{DEFAULT_BRANCH}}`

Replace these across all files before continuing.

### Step 2: Repositories

Ask:
- How many repositories does this project have?
- For each repo: name, directory name, git SSH URL, one-line description

The template ships with 3 repo rows (`REPO_1`, `REPO_2`, `REPO_3`). Adjust the tables:
- Fewer repos → remove extra rows from `CLAUDE.md`, `docs/repositories.md`, `docs/deployment.md`
- More repos → add rows following the same pattern

Replace per repo: `{{REPO_N_NAME}}`, `{{REPO_N_DIR}}`, `{{REPO_N_GIT_URL}}`, `{{REPO_N_DESCRIPTION}}`

After replacing, clone each repo into `repos/`:

```
git clone <git-url> repos/<dir-name>
```

If a repo is already cloned, skip it.

### Step 3: Per-Repo CLAUDE.md

For each cloned repo, check if it has a `CLAUDE.md` at its root.

**If it exists:** Read it and confirm with the user that it looks good. Move to the next repo.

**If it doesn't exist:** This step is optional — ask the user if they want to generate one.

If yes:
1. Analyze the repo structure — read key files, detect the tech stack, framework, directory layout, entry points, config files, test setup, and build commands
2. Draft a `CLAUDE.md` for the repo covering:
   - Tech stack and major dependencies
   - Architecture and directory structure
   - Key files and entry points
   - Common commands (build, test, lint, run)
   - Conventions (naming, file organization, code style observed)
   - Known gotchas if any are apparent
3. Present the draft to the user for review
4. Apply their feedback and write the file
5. Move to the next repo

If the user declines, move on — they can always add it later.

### Step 4: Architecture Overview

Once all repos are set up with their CLAUDE.md files, build the high-level architecture overview.

1. Read each repo's CLAUDE.md to understand what each repo does
2. Draft `docs/repositories.md` with:
   - The overview table (repo name, tech stack, deploy target, branch strategy) — ask the user for deploy target and branch strategy per repo if not already known
   - A Relationships section describing how the repos connect to each other (which repo serves the API, which are clients, shared libraries, etc.)
   - Any notes about the overall architecture
3. Present to the user for review and apply feedback

Also update the Relationships text in `docs/repositories.md` — don't leave the template example text ("serves the API consumed by..."). Write it based on the actual project structure.

### Step 5: Project Management

Ask:
- What tool do you use for tracking bugs and features? (Notion, Linear, Jira, GitHub Issues, etc.)
- Link to the board or project

Replace `{{PM_TOOL_DESCRIPTION}}` in `CLAUDE.md`. Format it like:
```
📋 **[Board Name](URL)** — description
```

If the user doesn't use a PM tool or doesn't want to set this up now, replace with `TODO` or remove the section.

### Step 6: Optional Configuration

After the core setup is complete, ask:

"The docs/ directory has template files for infrastructure, deployment, and emergency procedures. Want to fill any of these in now, or leave them for later?"

If the user wants to configure them, walk through the relevant `docs/*.md` files and replace their placeholders conversationally. If not, leave them as-is — the `{{...}}` placeholders serve as clear markers for what's left to do.

## After Setup

1. Run a final scan for any remaining `{{...}}` placeholders across all `.md` files
2. Print a summary:
   - Project name
   - Repos configured (with clone status)
   - Which repos have CLAUDE.md
   - Architecture overview status
   - Project management status
   - Count of remaining `TODO` or `{{...}}` items, if any
3. Remind the user: "You can re-run `/init` anytime to fill in remaining items."

## Important

- Never modify files inside `repos/` other than writing a new `CLAUDE.md` when the user approves it
- Never modify `.claude/skills/` — skills are not project configuration
- The `scripts/` table in `CLAUDE.md` starts empty — don't add placeholder scripts
- The `memory/` directory starts empty — don't add placeholder memories
- Preserve markdown formatting, table alignment, and section structure when replacing placeholders
- When cloning repos, if a clone fails (auth issues, wrong URL), tell the user and ask them to fix the URL before continuing
