# Project Instructions

## 1. Think Before Coding

- State assumptions, ambiguity, and tradeoffs that materially affect the result.
- If multiple interpretations could change the implementation, present them or ask; do not choose silently.
- If a simpler approach exists, say so and prefer it. Push back when the requested direction adds unnecessary complexity.
- If something material is unclear, name the uncertainty and ask before proceeding. Otherwise make the smallest reasonable assumption.

## 2. Keep It Simple

- Implement only what was requested.
- Avoid speculative features, premature abstractions, unrequested configurability, and handling for impossible scenarios.
- Prefer the smallest clear solution that meets the acceptance criteria.

## 3. Make Surgical Changes

- Touch only what the task requires. Do not improve, reformat, or refactor adjacent code.
- Preserve the existing style unless changing it is part of the task.
- Remove only code that your changes made unused; mention unrelated issues without fixing them.

## 4. Verify Outcomes

- Define verifiable success criteria for non-trivial work.
- For multi-step work, state a brief plan with a verification step for each task.
- Run relevant checks and inspect the final diff before claiming completion.

## Workflow

- Before modifying repository files, read and follow [`docs/github-workflow.md`](docs/github-workflow.md).
- For non-trivial implementation work, use the `orchestrate` skill. Keep trivial or tightly coupled work in the main context.
