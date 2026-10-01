# 아키텍처

FastAPI 기반 서버 렌더링 웹 애플리케이션이며, Jinja2 템플릿과 SQLite를 사용합니다.
프론트엔드 프레임워크는 사용하지 않고 순수 CSS와 최소한의 JavaScript만 사용합니다.

## 기술 스택

| 계층 | 기술 |
| --- | --- |
| 웹 프레임워크 | FastAPI |
| 템플릿 | Jinja2 (서버 렌더링) |
| 데이터 | SQLite (WAL 모드, 표준 라이브러리 sqlite3) |
| 시드 데이터 | Faker (첫 실행 시 자동 생성) |
| 스타일 | 순수 CSS (static/css/style.css, CSS 변수 기반 다크 모드) |
| 실행 | uvicorn |

## 계층 구조

세 개의 계층으로 구분하며, 역할을 혼합하지 않습니다.

- **`app/routers/`** — HTTP 라우트. 요청 파싱, 권한 검사, 템플릿 렌더링만 담당
- **`app/services/`** — 비즈니스 로직과 모든 데이터베이스 접근
- **`app/core/`** — 인프라: DB 연결(db.py), 인증(auth.py), 시드(seed.py), 템플릿 설정(templating.py)

라우터에서 SQL을 직접 실행하지 마세요. 데이터 접근은 반드시 services 계층을 거칩니다.

## 작업별 파일 위치

| 작업 | 위치 |
| --- | --- |
| 새 페이지 추가 | `app/routers/`에 라우트 추가 + `templates/`에 템플릿 추가 + `main.py`에 라우터 등록 |
| 공통 레이아웃 수정 | `templates/base.html`, `templates/partials/` |
| 인증 로직 | `app/core/auth.py` |
| 채용공고 / 지원 로직 | `app/services/job_service.py`, `app/services/misc_services.py` |
| 프로필 로직 | `app/services/profile_service.py` |
| 스키마 변경 | `app/core/db.py` (SCHEMA) |
| 시드 데이터 수정 | `app/core/seed.py` |
