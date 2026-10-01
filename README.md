# CLAUDE.md Template

A minimal `CLAUDE.md` for Claude Code: the [ponytail](https://github.com/DietrichGebert/ponytail) plugin carries the coding rules, and this file carries only the facts about your repository that no plugin can know.

## Why it's short

Claude Code loads `CLAUDE.md` at the start of every session as override-priority instructions. Restating something Claude already does by default doesn't reinforce it — it competes with the rules that actually matter. [Anthropic's guidance](https://code.claude.com/docs/en/best-practices) is blunt about the result: *"Bloated CLAUDE.md files cause Claude to ignore your actual instructions."*

So every line passes one test:

> **Would removing this cause Claude to make mistakes?** If not, cut it.

Rules that only restate default behavior — *state your assumptions*, *implement only what was requested*, *match the existing style* — are left out. So are the minimalism principles this template used to carry (push back on complexity, keep the diff traceable, turn tasks into checkable goals, never cut validation/security/accessibility): ponytail injects the same rules every session through a hook, and measured better — see [Why ponytail carries the rules](#why-ponytail-carries-the-rules). What is left is **Workflow** and **Project facts**.

## Start with ponytail, globally

This template assumes ponytail is on. Install it once at user scope so every repository gets it (two separate prompts):

```
/plugin marketplace add DietrichGebert/ponytail
/plugin install ponytail@ponytail
```

A new session then starts with `PONYTAIL MODE ACTIVE — level: full`. Do not add minimalism rules to `CLAUDE.md` on top of it: stacking rules on the plugin was measured to cost more, not less.

## Use it

Three files, and only the first is required:

| File | Copy it when | Why |
| --- | --- | --- |
| [`CLAUDE.md`](CLAUDE.md) | always | Workflow + Project facts |
| [`docs/github-workflow.md`](docs/github-workflow.md) | you keep the **Workflow** section | the project file links to it; without the file the link is dead |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE) | you track work as GitHub issues | backs the issue rules under **Workflow** |

```sh
src=$(mktemp -d)
git clone --depth 1 https://github.com/seanjeonn/my-claude-md.git "$src"
cd /path/to/your-project   # replace with your project's path

cp "$src/CLAUDE.md" .

# optional, only if you keep the Workflow section
mkdir -p docs .github && cp "$src/docs/github-workflow.md" docs/
cp -r "$src/.github/ISSUE_TEMPLATE" .github/
```

Then:

1. **Fill in Project facts.** That section is the most valuable part and the only one a template can't write for you: build and test commands, environment quirks, and gotchas Claude can't infer from the code. Run `/init` in Claude Code to draft them from your codebase, then prune what it guesses.
2. **Drop what you skipped.** If you didn't copy the workflow file or the issue templates, delete the matching bullets under **Workflow** — a rule pointing at a file that isn't there is worse than no rule.
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

## Why ponytail carries the rules

Measured (2026-09, headless Claude Code, 12 multi-file tickets on `fastapi/full-stack-fastapi-template`, paired blocks, pre-registered protocol):

| Condition vs no instructions | claude-fable-5-1 (n = 3/task) | claude-haiku-4-5 (n = 4/task) |
| --- | --- | --- |
| this template's earlier principle-based `CLAUDE.md` (commit `8cc4bd8`) | LOC −51% (95% CI −72 … −25), cost −32% | LOC +1% (CI −20 … +27) — no effect |
| ponytail plugin | LOC −61% (CI −78 … −38), cost −44% | LOC −43% (CI −63 … −19) |
| ponytail **+** a 5-rule project `CLAUDE.md` | cost **+83%** (CI +41 … +137) vs ponytail alone | not distinguishable from ponytail alone at n = 12 |

Three things follow. The principle-based file worked on the larger model and did nothing on the small one; ponytail beat it on every metric on both; and stacking "do more" rules on top of ponytail made the larger model do more — longer agentic loops, not better code — while a blind completeness/never-cut grading found no quality gain that survived its own noise. So the project file carries facts, not principles, and the principles live in the plugin. Full write-up and raw data: the `claude-bench` harness (private).

## Keep it pruned

Two signals that the file needs work:

- **Claude repeatedly breaks a rule that is written down** — the file is too long and the rule is getting lost.
- **Claude asks something the file already answers** — the wording is ambiguous.

Treat it like code: review it when things go wrong, and test changes by watching whether behavior actually shifts.

## License

MIT
