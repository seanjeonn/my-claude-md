# GitHub Workflow

## 릴리즈 태깅

- main으로 릴리즈가 머지되면 해당 머지 커밋에 SemVer 형식의 annotated tag를 붙인다: `vMAJOR.MINOR.PATCH` (예: `v1.2.0`).
- 태그 생성과 푸시:

  ```sh
  git tag -a vX.Y.Z -m "release vX.Y.Z" <merge-commit>
  git push origin vX.Y.Z
  ```

- 버전 증가 기준: 호환성이 깨지는 변경은 MAJOR, 기능 추가는 MINOR, 수정·문서만이면 PATCH.
- 태그는 릴리즈된 main 커밋에만 붙인다. 릴리즈가 아닌 일반 머지에는 붙이지 않는다.
