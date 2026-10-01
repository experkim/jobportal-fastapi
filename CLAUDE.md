# CLAUDE.md

이 파일은 Claude Code가 이 저장소에서 작업할 때 따라야 할 지침을 제공합니다.

## 명령어

- `uvicorn main:app --reload` — 개발 서버 실행 (http://127.0.0.1:8000)
- `pip install -r requirements.txt` — 의존성 설치
- `pytest` — 테스트 실행
- `ruff check .` — 린트 / `ruff format` — 포맷팅

## 저장소 구조

```text
jobportal-fastapi/
├── main.py               # 앱 조립: 라우터 등록, lifespan(스키마+시드)
├── app/
│   ├── core/             # 인프라: db, auth(세션·역할), seed, templating
│   ├── routers/          # HTTP 라우트 (권한 검사 + 렌더링만)
│   └── services/         # 비즈니스 로직 + 모든 DB 접근
├── templates/            # Jinja2 (base.html 상속, partials/, admin/)
├── static/               # css/style.css (CSS 변수·다크모드), js/main.js
└── jobportal.db          # SQLite (첫 실행 시 자동 생성·시드)
```

## 데모 계정

admin@demo.com/admin123 · employer@demo.com/employer123 · seeker@demo.com/seeker123

## Git

- 브랜치: feature/ · fix/ · docs/ 접두사, main에서 분기
- 커밋 메시지 형식: `fix: resolve tooltip overflow on footer links`
  (접두사 + 콜론 + 현재시제 소문자, 마침표 없음, 72자 이내)
- main에 직접 push 금지. 항상 PR로
- 커밋 전 `pytest`와 `ruff check .` 실행

## 세부 규칙

세부 규칙은 `.claude/rules/`에 주제별로 분리되어 있습니다.

| 파일 | 내용 | 로드 시점 |
| --- | --- | --- |
| `architecture.md` | 기술 스택, 계층 구조, 작업별 파일 위치 | 항상 |
| `coding-standards.md` | 언어·네이밍·템플릿/스타일·린트 규칙 | 항상 |
| `git-conventions.md` | 브랜치·커밋·PR 규칙 | 항상 |
| `data-layer.md` | 서비스 계층, SQLite 사용, 스키마 변경 | `app/services/`, `db.py`, `seed.py` 작업 시 |
| `routing-roles.md` | 역할 정의, 라우트 보호, 라우팅 컨벤션 | `app/routers/`, `auth.py`, `templates/` 등 작업 시 |
