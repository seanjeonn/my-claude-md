# CLAUDE.md Template

A minimal `CLAUDE.md` for Claude Code, containing only rules that are not already default behavior.

## Why it's short

Claude Code loads `CLAUDE.md` at the start of every session as override-priority instructions. Restating something Claude already does by default doesn't reinforce it — it competes with the rules that actually matter. [Anthropic's guidance](https://code.claude.com/docs/en/best-practices) is blunt about the result: *"Bloated CLAUDE.md files cause Claude to ignore your actual instructions."*

So every line passes one test:

> **Would removing this cause Claude to make mistakes?** If not, cut it.

Rules that survive carry a checkable test next to them. Rules that only restate default behavior — *state your assumptions*, *implement only what was requested*, *match the existing style* — are left out on purpose.

One limit, measured: the rules in `CLAUDE.md` move the larger Claude models and do nothing on the small ones (see [With ponytail](#with-ponytail)). If your sessions run on a Haiku-class model, a plugin that injects its rules through a hook is what works, not this file.

## Start with ponytail, globally

Install the [ponytail](https://github.com/DietrichGebert/ponytail) plugin once at user scope, so every repository gets it. It is the single largest measured win in this setup, and it is where the minimalism rules should live — not in a per-project file:

```
/plugin marketplace add DietrichGebert/ponytail
/plugin install ponytail@ponytail
```

(two separate prompts). Then pick the project file by whether ponytail is on:

| ponytail installed? | Copy as your project `CLAUDE.md` | What it carries |
| --- | --- | --- |
| yes (recommended) | [`CLAUDE.with-ponytail.md`](CLAUDE.with-ponytail.md) | **Workflow** + **Project facts** only |
| no | [`CLAUDE.md`](CLAUDE.md) | the three principles, *Never cut*, Workflow, Project facts |

Do not use `CLAUDE.md` with ponytail: it restates rules ponytail already injects, and stacking rules on top of the plugin was measured to cost more, not less.

## Use it

Three files, and only the first is required:

| File | Copy it when | Why |
| --- | --- | --- |
| [`CLAUDE.with-ponytail.md`](CLAUDE.with-ponytail.md) or [`CLAUDE.md`](CLAUDE.md) | always — pick one per the table above | the rules themselves |
| [`docs/github-workflow.md`](docs/github-workflow.md) | you keep the **Workflow** section | the project file links to it; without the file the link is dead |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE) | you track work as GitHub issues | backs the "link work to a tracking issue" rule |

```sh
git clone --depth 1 https://github.com/seanjeonn/my-claude-md.git /tmp/my-claude-md
cd /path/to/your-project

cp /tmp/my-claude-md/CLAUDE.with-ponytail.md CLAUDE.md   # with ponytail (recommended)
# cp /tmp/my-claude-md/CLAUDE.md .                       # without ponytail

# optional, only if you keep the Workflow section
mkdir -p docs .github && cp /tmp/my-claude-md/docs/github-workflow.md docs/
cp -r /tmp/my-claude-md/.github/ISSUE_TEMPLATE .github/
```

Then:

1. **Fill in Project facts.** That section is the most valuable part and the only one a template can't write for you: build and test commands, environment quirks, and gotchas Claude can't infer from the code. Run `/init` in Claude Code to draft them from your codebase, then prune what it guesses.
2. **Drop what you skipped.** If you didn't copy the workflow file or the issue templates, delete the matching bullet under **Workflow** — a rule pointing at a file that isn't there is worse than no rule.
3. **Check it loaded.** Start a session and run `/memory`; the project `CLAUDE.md` should be listed.

## Skills or Plugins

Installed separately at user scope — not part of this template. This is what actually runs alongside it:

| Skill or plugin | Use it for | Source |
| --- | --- | --- |
| **ponytail** | Writing less code: reuse, stdlib, native features before anything new. Global, always on; measured LOC −61% / cost −44% on claude-fable-5-1 and still effective on Haiku | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) |
| **claude-md-management** | Maintaining the project file: audits it against the codebase, and `/revise-claude-md` folds session learnings back in | [anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/claude-md-management) |
| **gstack** (office-hours only) | `/office-hours` for product and scope questions. The rest of the suite is disabled: 50+ always-resident skill descriptions were not worth their context | [garrytan/gstack](https://github.com/garrytan/gstack) |
| **eli5** | `/eli5 <topic>` — explains anything as a picture-first HTML artifact with big visuals and few words | [anthropics/claude-plugins-community](https://github.com/anthropics/claude-plugins-community/tree/main/eli5) |

Tried and set aside: [superpowers](https://github.com/obra/superpowers) (overlaps ponytail once that is global), [graphify](https://github.com/Graphify-Labs/graphify) (useful only on a large monorepo; not global), [taste-skill](https://github.com/Leonxlnx/taste-skill) (never adopted).

## With ponytail

The reason the project file drops the principles when ponytail is on: ponytail already injects the same rules (reuse first, stdlib, one runnable check, never cut validation/security/accessibility) every session through a hook, and it does so more effectively.

Why, measured (2026-09, headless Claude Code, 12 multi-file tickets on `fastapi/full-stack-fastapi-template`, paired blocks, pre-registered protocol):

| Condition vs no instructions | claude-fable-5-1 (n = 3/task) | claude-haiku-4-5 (n = 4/task) |
| --- | --- | --- |
| `CLAUDE.md` from this repo | LOC −51% (95% CI −72 … −25), cost −32% | LOC +1% (CI −20 … +27) — no effect |
| ponytail plugin | LOC −61% (CI −78 … −38), cost −44% | LOC −43% (CI −63 … −19) |
| ponytail **+** a 5-rule project `CLAUDE.md` | cost **+83%** (CI +41 … +137) vs ponytail alone | not distinguishable from ponytail alone at n = 12 |

Three things follow. This file alone works on the larger model and does nothing on the small one. ponytail beats it on every metric on both. Stacking "do more" rules on top of ponytail made the larger model do more — longer agentic loops, not better code — while a blind completeness/never-cut grading found no quality gain that survived its own noise. So with ponytail, the project file should carry facts, not principles. Full write-up and raw data: the `claude-bench` harness (private).

## Keep it pruned

Two signals that the file needs work:

- **Claude repeatedly breaks a rule that is written down** — the file is too long and the rule is getting lost.
- **Claude asks something the file already answers** — the wording is ambiguous.

Treat it like code: review it when things go wrong, and test changes by watching whether behavior actually shifts.

## License

MIT
