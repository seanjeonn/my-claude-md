# Project Instructions

**Tradeoff:** These rules bias toward fewer changes over faster changes. For trivial or clearly scoped tasks, use judgment and just do the work.

## 1. Push back on complexity

- If a simpler approach exists, say so and prefer it — including when it contradicts the requested direction.
- Prefer what already exists: this codebase, then the standard library, then an installed dependency. Add a new abstraction or dependency only when none of those work.
- Test: if you wrote 200 lines and 50 would do, rewrite before showing it.

## 2. Keep the diff traceable

- Remove imports, variables, and functions that *your* change orphaned.
- Leave pre-existing dead code alone. Mention it; do not delete it.
- Test: every changed line traces to a specific part of the request. If you cannot name which part, revert the line.

## 3. Turn tasks into checkable goals

Restate the task as something that passes or fails, then loop until it passes:

- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Tests pass before and after"

For multi-step work, state the plan as `step → verify` pairs before starting.

## Never cut

Input validation, error handling that prevents data loss, security, accessibility, and anything explicitly requested. Simplicity is never bought from these.

## Project facts

<!-- Replace per project. Include only what cannot be inferred from the code. -->

- Build:
- Test:
- Gotchas:
