---
paths:
  - "app/services/**/*.py"
  - "app/core/db.py"
  - "app/core/seed.py"
---

# 데이터 계층 규칙

## 서비스 계층 원칙

- 모든 데이터베이스 접근은 `app/services/`의 서비스 함수를 통해서만 수행합니다.
- 라우터는 서비스 함수를 호출할 뿐, SQL을 직접 실행하지 않습니다.
- 서비스 함수는 sqlite3.Row(또는 그 리스트)를 반환하고, 표현(포맷팅)은 템플릿에 맡깁니다.

## SQLite 사용 규칙

- 연결은 항상 `app/core/db.py`의 `get_db()`로 얻습니다 (WAL 모드·row_factory 설정 포함).
- 연결은 `try/finally`로 반드시 `conn.close()` 합니다.
- SQL 값 삽입은 **반드시 파라미터 바인딩(`?`)**을 사용합니다. f-string으로 값을 조립하지 마세요 (SQL 인젝션 방지).
- 쓰기 작업 후에는 `conn.commit()`을 잊지 마세요.

## 스키마 변경

- 테이블 추가·변경은 `app/core/db.py`의 SCHEMA 문자열에서만 수행합니다.
- 시드 데이터가 필요한 변경이면 `app/core/seed.py`도 함께 갱신합니다.
- 개발 중 스키마가 바뀌면 `jobportal.db` 파일을 삭제하고 재실행하면 재생성됩니다.
