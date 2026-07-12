# GitHub Workflow

## Long-Lived Branches

| Branch    | Purpose                                |
| --------- | -------------------------------------- |
| `main`    | Production-ready code                  |
| `develop` | Integration branch deployed to staging |

Never commit or push directly to `main` or `develop`. All changes must be merged through pull requests.

## Working Branches

Before modifying files, ensure the task has its own worktree and branch.

Name branches using:

```text
<type>/<scope>-<description>
```

Use lowercase kebab-case for the scope and description.

| Type        | Base      | Merge Target |
| ----------- | --------- | ------------ |
| `feature/*` | `develop` | `develop`    |
| `fix/*`     | `develop` | `develop`    |
| `chore/*`   | `develop` | `develop`    |
| `hotfix/*`  | `main`    | `main`       |

After merging a hotfix into `main`, propagate the same fix to `develop` through a pull request.

## Issues

- Before implementation, link the work to a Feature, Bug Report, or implementation sub-issue.
- Use a **Feature** issue for approved, multi-step work. Track its implementation with sub-issues.
- Use a **Bug Report** for reproducible problems or unexpected behavior.
- Use a **Work Proposal** for candidate work discovered through reviews, analysis, or deferred scope.
- When a proposal is accepted, create and link a Feature issue for its implementation.
- Never include secrets or exploitable security details in a public issue.

## Commits and Pull Requests

Use `.github/pull_request_template.md` when opening a pull request.

Commit messages and pull request titles must follow Conventional Commits:

```text
<type>(<scope>): <description>
```

Examples:

```text
feat(auth): add OAuth login
fix(api): handle request timeout
chore(deps): update ESLint
```

Run relevant checks before pushing. Remove the worktree only after its changes are merged or discarded.
