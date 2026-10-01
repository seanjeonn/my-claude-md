# GitHub Workflow

## Release tagging

- When a release is merged into main, put a SemVer annotated tag on that merge commit: `vMAJOR.MINOR.PATCH` (e.g. `v1.2.0`).
- Create and push the tag:

  ```sh
  git tag -a vX.Y.Z -m "release vX.Y.Z" <merge-commit>
  git push origin vX.Y.Z
  ```

- Version bump: breaking changes are MAJOR, new features are MINOR, fixes or docs only are PATCH.
- Tag only released main commits. Do not tag ordinary, non-release merges.
