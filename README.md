# CLAUDE.md Template

A minimal `CLAUDE.md` for Claude Code, containing only rules that are not already default behavior.

## Why it's short

Claude Code loads `CLAUDE.md` at the start of every session as override-priority instructions. Restating something Claude already does by default doesn't reinforce it — it competes with the rules that actually matter. [Anthropic's guidance](https://code.claude.com/docs/en/best-practices) is blunt about the result: *"Bloated CLAUDE.md files cause Claude to ignore your actual instructions."*

So every line passes one test:

> **Would removing this cause Claude to make mistakes?** If not, cut it.

Rules that survive carry a checkable test next to them. Rules that only restate default behavior — *state your assumptions*, *implement only what was requested*, *match the existing style* — are left out on purpose.

## Use it

Copy [`CLAUDE.md`](CLAUDE.md) into your project root and fill in **Project facts**. That section is the most valuable part and the only one a template can't write for you: build and test commands, environment quirks, and gotchas Claude can't infer from the code.

Run `/init` in Claude Code to draft those facts from your codebase, then prune what it guesses.

## Skills

Installed separately — not part of this template. Listed so a new project starts with them in mind.

| Skill | Use it for | Source |
| --- | --- | --- |
| **superpowers** | General methodology: planning, TDD, debugging, and skill authoring itself | [obra/superpowers](https://github.com/obra/superpowers) |
| **gstack** | An opinionated end-to-end setup — discovery, design, release, docs, and QA as slash commands | [garrytan/gstack](https://github.com/garrytan/gstack) |
| **graphify** | Understanding a codebase: turns code, docs, and papers into a queryable knowledge graph | [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) |
| **ponytail** | Writing less code: reuse, stdlib, and native features before anything new | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) |
| **taste-skill** | Frontend and design work — layout, typography, motion, and spacing that doesn't look generated | [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) |

## Keep it pruned

Two signals that the file needs work:

- **Claude repeatedly breaks a rule that is written down** — the file is too long and the rule is getting lost.
- **Claude asks something the file already answers** — the wording is ambiguous.

Treat it like code: review it when things go wrong, and test changes by watching whether behavior actually shifts.

## License

MIT
