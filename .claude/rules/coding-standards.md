# 코딩 표준

## 언어 및 구조

- Python 3.11+ 기준으로 작성하며 PEP 8을 따릅니다.
- 함수 시그니처에는 타입 힌트 사용을 권장합니다.
- 모든 모듈 첫 줄에 한 줄 docstring을 작성합니다.
- 하나의 파일이 500줄을 넘지 않게 유지합니다 (훅으로 강제됨).

## 네이밍 규칙

- 함수·변수: `snake_case`
- 클래스: `PascalCase`
- 상수: `UPPER_SNAKE_CASE`
- 템플릿 파일: `snake_case.html`

## 템플릿과 스타일

- 모든 페이지 템플릿은 `base.html`을 extends 합니다.
- 스타일은 `static/css/style.css`의 CSS 변수(`var(--...)`)만 사용합니다. inline style 금지.
- 다크 모드는 `html[data-theme]` 속성 전환 방식입니다. 새 색상은 반드시 라이트/다크 두 팔레트에 추가하세요.

## 린트

- `ruff check .`로 검사하고 `ruff format`으로 포맷팅합니다.
