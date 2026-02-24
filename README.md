# aw-pack

An installable [GitHub Agentic Workflows](https://github.github.io/gh-aw/) pack providing five AI-powered repository assistants. Works with any GitHub repository out of the box and improves with project-specific customization.

## Workflows

| Workflow | Trigger | What it does |
|---|---|---|
| **issue-triage** | New/reopened issues | Labels issues by category and component, posts triage comment |
| **pr-review** | New/updated PRs | Runs build/tests, reviews against conventions, flags breaking changes |
| **weekly-status** | Weekly on Monday | Creates a status issue with metrics and actionable maintainer suggestions |
| **doc-sync** | Push to main | Detects stale documentation, opens draft PRs to fix it |
| **repo-assist** | Daily + `/repo-assist` command | Nudges stale PRs, welcomes contributors, fixes CI, manages labels |

All workflows use **Claude** as the AI engine. They run with read-only permissions by default - all write operations go through rate-limited safe-outputs.

## Installation

### Prerequisites

- [GitHub CLI](https://cli.github.com/) v2.0.0+
- [gh-aw extension](https://github.com/github/gh-aw): `gh extension install github/gh-aw`
- An Anthropic API key

### Install all workflows

```bash
gh aw add "srdjan/aw-pack/*"
gh aw secrets set ANTHROPIC_API_KEY
gh aw compile
```

### Install a single workflow

```bash
gh aw add srdjan/aw-pack/repo-assist
gh aw secrets set ANTHROPIC_API_KEY
gh aw compile
```

## Customization

After installation, edit `.github/workflows/shared/repo-context.md` to describe your project. This single file is imported by all five workflows. It has four sections:

1. **Project** - name, description, language, package identifier
2. **Architecture** - modules/layers with their source file paths
3. **Component Labels** - project-specific labels beyond the generic set
4. **Conventions and Build Commands** - coding standards and build/test/lint commands

Without customization, the workflows still work - the AI agent discovers project context at runtime by reading README.md, package.json, and other standard files. Customization makes the agent faster and more consistent.

See `examples/repo-context-metador.md` for a filled-in example.

### Adding custom labels

The `safe-outputs` in each workflow define an allowlist of labels the agent can apply. After customization, add your project-specific labels to the YAML frontmatter of the relevant workflows (`issue-triage.md`, `pr-review.md`, `repo-assist.md`).

### Trimming bash commands

The `pr-review`, `doc-sync`, and `repo-assist` workflows include build/test commands for all major ecosystems (Node, Deno, Cargo, Python, Go, Ruby, Make). After installation, you can trim this list to only your project's commands.

## Updating

When the pack gets updates:

```bash
gh aw update              # update all workflows, preserving local customizations
gh aw update repo-assist  # update a single workflow
```

The update performs a 3-way merge: your local changes are preserved alongside upstream updates.

## Security

- All workflows run with **read-only permissions** by default
- Write operations (labels, comments, PRs, reviews) go through **safe-outputs** with rate limits
- Bash commands are **allowlisted** - only build/test/lint commands, not arbitrary execution
- The repo-assist workflow creates only **draft PRs** - a maintainer must review before merge
- Agent disclosure: every public comment begins with an automated notice

## Engine

All workflows default to `engine: claude`. To use a different engine, edit the frontmatter:

```yaml
engine: copilot   # GitHub Copilot
engine: codex     # OpenAI Codex
engine: gemini    # Google Gemini
```

And set the corresponding secret:

```bash
gh aw secrets bootstrap --engine copilot
```
