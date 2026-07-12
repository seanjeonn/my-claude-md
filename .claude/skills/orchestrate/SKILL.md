---
name: orchestrate
description: Use when starting non-trivial implementation work that benefits from planning, delegation, model routing, or independent verification
---

# Orchestrate Work

Keep ownership of planning, user communication, integration, and final verification in the main conversation.

## Plan

Use Claude Code's native Plan mode and built-in Plan agent before modifying files. Define the objective, scope, acceptance criteria, tasks, risks, and verification. Wait for user approval before implementation.

## Route

Use one agent by default. Delegate only bounded work when specialization, context isolation, or parallel execution provides a clear benefit.

| Work | Primary | Fallback |
| --- | --- | --- |
| Plan review or product judgment | Fable | Opus |
| Clear coding or investigation | Codex through `/codex:rescue` | Sonnet |
| Code review | `/codex:review` | Fable or Opus |
| Design challenge | `/codex:adversarial-review` | Fable or Opus |
| Mechanical checks | Cheapest reliable model | Main conversation |

Before external delegation, verify that the adapter is available and authenticated. Do not install or authenticate tools without approval. Delegation is read-only by default; allow writes only for an approved implementation in its assigned worktree.

Give each worker the objective, scope, relevant context, constraints, expected output, and success criteria. Workers must not delegate back to the caller. Do not enable automatic cross-provider review gates.

## Execute

Follow [`docs/github-workflow.md`](../../../docs/github-workflow.md). Parallelize only independent tasks with non-overlapping write scopes. Keep shared and integration changes in the main conversation.

## Verify

Check the acceptance criteria, relevant tests, final diff, and repository state. Use one independent review for high-risk, security-sensitive, architectural, or user-facing changes. If verification fails, retry once with specific feedback, then escalate the model or return control to the user.

## Learn

Record reusable follow-up only when warranted:

- Reproducible defect: Bug Report and regression test
- Repeated preventable mistake: focused instruction, test, or automation
- Security, business, technical, deferred, or out-of-scope work: Work Proposal
- One-off environment problem: pull request validation note
