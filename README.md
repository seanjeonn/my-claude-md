# Claude Code Workflow Template

A minimal, opinionated template for planning, delegating, implementing, and reviewing software work with Claude Code.

## What's Included

| Path | Purpose |
| --- | --- |
| [`CLAUDE.md`](CLAUDE.md) | Core rules loaded for every Claude Code session |
| [`.claude/skills/orchestrate/SKILL.md`](.claude/skills/orchestrate/SKILL.md) | Plan, model routing, execution, verification, and follow-up workflow |
| [`docs/github-workflow.md`](docs/github-workflow.md) | Worktree, branch, issue, commit, and pull request rules |
| [`.github/ISSUE_TEMPLATE`](.github/ISSUE_TEMPLATE) | Feature, bug report, and work proposal forms |
| [`.github/pull_request_template.md`](.github/pull_request_template.md) | Pull request summary and validation checklist |

## Workflow

For non-trivial implementation work, the orchestrator follows five stages:

1. **Plan** — Use Claude Code's native Plan mode and wait for approval.
2. **Route** — Select the smallest capable worker and delegate only bounded tasks.
3. **Execute** — Work in an isolated branch and worktree.
4. **Verify** — Check acceptance criteria, tests, the final diff, and repository state.
5. **Learn** — Record reproducible defects, preventable mistakes, and deferred work in the appropriate durable form.

Trivial or tightly coupled work stays in the main conversation.

## Use This Template

### Option A — Clone as a new project

Start a fresh project from this repository, then detach it from this history:

```bash
git clone https://github.com/seanjeonn/my-claude-md.git my-project
cd my-project
rm -rf .git
git init
```

`rm -rf .git` removes the template's commit history so `git init` starts your own. Point the new repository at your own remote when you create it.

### Option B — Copy into an existing project

Copy or merge these paths into the root of an existing project:

```text
CLAUDE.md
.claude/skills/orchestrate/SKILL.md
docs/github-workflow.md
.github/
```

### After either option

Review the two project-specific policies:

- Update the model routing table in the `orchestrate` skill for the models and adapters available in your environment.
- Update `docs/github-workflow.md` if your branch strategy or merge targets differ.

Claude Code loads `CLAUDE.md` as project instructions and discovers project skills from `.claude/skills`.

## Optional Codex Integration

The default routing uses [OpenAI's Codex plugin for Claude Code](https://github.com/openai/codex-plugin-cc) for delegated implementation and independent review. Install and authenticate it separately if you want to use those routes.

Without the plugin, the orchestrator falls back to the available Claude models defined in the skill.

## GitHub Setup

The included issue forms expect `feature`, `bug`, and `proposal` labels. Create or rename those labels to match your repository.

The workflow instructions do not enforce repository permissions. Configure GitHub branch protection or rulesets separately to prevent direct pushes to `main` and `develop`.
