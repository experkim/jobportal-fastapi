# Git 규칙

## 브랜치 규칙

브랜치 이름은 작업 목적에 따라 다음과 같은 형식을 사용합니다.

```text
feature/add-job-filter-sidebar         # 새로운 기능 추가
fix/employer-route-redirect-loop       # 버그 수정
docs/update-readme                     # 문서 수정
chore/upgrade-dependencies             # 유지보수 및 개발 도구 관련 작업
refactor/simplify-auth-session         # 코드 리팩터링
style/mobile-job-card-spacing          # UI 스타일 및 디자인 수정
```

- 모든 새로운 작업은 `main` 브랜치에서 분기합니다.
- 브랜치는 가능한 한 짧은 기간 동안 유지하고, 작업이 완료되면 PR(Pull Request)을 생성합니다.
- PR이 병합된 후에는 작업 브랜치를 삭제합니다.

## 커밋 메시지 규칙

커밋 메시지는 **Conventional Commits** 형식을 따릅니다.

```text
feat: add saved jobs count to navbar
fix: correct role guard on employer routes
docs: update README with demo credentials
chore: upgrade fastapi to latest
refactor: extract job card into shared template partial
style: fix spacing on mobile job list
```

주요 커밋 유형은 다음과 같습니다.

- `feat`: 새로운 기능 추가
- `fix`: 버그 수정
- `docs`: 문서 수정
- `chore`: 의존성 업데이트, 설정 변경 등 유지보수 작업
- `refactor`: 기능 변경 없이 코드 구조 개선
- `style`: UI 스타일, 레이아웃 등 시각적 요소 수정

커밋 메시지 작성 시 다음 규칙을 따릅니다.

- 현재형을 사용합니다.
- 영문 소문자로 작성합니다.
- 제목 끝에 마침표(`.`)를 사용하지 않습니다.
- 제목은 72자 이내로 작성합니다.
- 변경 내용이 명확하지 않거나 추가 설명이 필요한 경우 커밋 본문(body)을 작성합니다.
- main에 직접 push 금지. 항상 PR로
- 커밋 전 `pytest`와 `ruff check .` 실행

## Pull Request 규칙

- PR 제목은 **Conventional Commits** 형식을 따릅니다.

```text
feat: add saved jobs count to navbar
fix: correct role guard on employer routes
```

- PR 설명에는 다음 내용을 포함합니다.
  - 변경 사항 요약(Summary)
  - 테스트 방법 및 결과(Test Plan)

- PR의 대상(base) 브랜치는 `main`으로 설정합니다.
