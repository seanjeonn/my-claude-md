# CLAUDE.md Template

A minimal `CLAUDE.md` for Claude Code, containing only rules that are not already default behavior.

## Why it's short

Claude Code loads `CLAUDE.md` at the start of every session as override-priority instructions. Restating something Claude already does by default doesn't reinforce it — it competes with the rules that actually matter. [Anthropic's guidance](https://code.claude.com/docs/en/best-practices) is blunt about the result: *"Bloated CLAUDE.md files cause Claude to ignore your actual instructions."*

So every line passes one test:

> **Would removing this cause Claude to make mistakes?** If not, cut it.

Rules that survive carry a checkable test next to them. Rules that only restate default behavior — *state your assumptions*, *implement only what was requested*, *match the existing style* — are left out on purpose.

## Use it

Three files, and only the first is required:

| File | Copy it when | Why |
| --- | --- | --- |
| [`CLAUDE.md`](CLAUDE.md) | always | the rules themselves |
| [`docs/github-workflow.md`](docs/github-workflow.md) | you keep the **Workflow** section | `CLAUDE.md` links to it; without the file the link is dead |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE) | you track work as GitHub issues | backs the "link work to a tracking issue" rule |

```sh
git clone --depth 1 https://github.com/seanjeonn/my-claude-md.git /tmp/my-claude-md
cd /path/to/your-project

cp /tmp/my-claude-md/CLAUDE.md .

# optional, only if you keep the Workflow section
mkdir -p docs .github && cp /tmp/my-claude-md/docs/github-workflow.md docs/
cp -r /tmp/my-claude-md/.github/ISSUE_TEMPLATE .github/
```

Then:

1. **Fill in Project facts.** That section is the most valuable part and the only one a template can't write for you: build and test commands, environment quirks, and gotchas Claude can't infer from the code. Run `/init` in Claude Code to draft them from your codebase, then prune what it guesses.
2. **Drop what you skipped.** If you didn't copy the workflow file or the issue templates, delete the matching bullet under **Workflow** — a rule pointing at a file that isn't there is worse than no rule.
3. **Check it loaded.** Start a session and run `/memory`; the project `CLAUDE.md` should be listed.

## Skills or Plugins

Installed separately — not part of this template. Listed so a new project starts with them in mind.

| Skill or plugin | Use it for | Source |
| --- | --- | --- |
| **claude-md-management** | Maintaining this file: audits `CLAUDE.md` against the codebase, and `/revise-claude-md` folds session learnings back in | [anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/claude-md-management) |
| **superpowers** | General methodology: planning, TDD, debugging, and skill authoring itself | [obra/superpowers](https://github.com/obra/superpowers) |
| **gstack** | An opinionated end-to-end setup — discovery, design, release, docs, and QA as slash commands | [garrytan/gstack](https://github.com/garrytan/gstack) |
| **graphify** | Understanding a codebase: turns code, docs, and papers into a queryable knowledge graph | [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) |
| **ponytail** | Writing less code: reuse, stdlib, and native features before anything new | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) |
| **taste-skill** | Frontend and design work — layout, typography, motion, and spacing that doesn't look generated | [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) |
| **eli5** | `/eli5 <topic>` — explains anything as a picture-first HTML artifact with big visuals and few words | [anthropics/claude-plugins-community](https://github.com/anthropics/claude-plugins-community/tree/main/eli5) |

## Keep it pruned

Two signals that the file needs work:

- **Claude repeatedly breaks a rule that is written down** — the file is too long and the rule is getting lost.
- **Claude asks something the file already answers** — the wording is ambiguous.

Treat it like code: review it when things go wrong, and test changes by watching whether behavior actually shifts.

## License

MIT
