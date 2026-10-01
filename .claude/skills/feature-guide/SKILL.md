---
name: feature-guide
description: 특정 JobPortal 기능이 라우터에서 서비스, 데이터 계층, 템플릿까지 전체적으로 어떻게 동작하는지 설명합니다.
argument-hint: <feature-name>
user-invocable: true
disable-model-invocation: false
context: fork
agent: Explore
---

## 역할

당신은 JobPortal 코드베이스를 속속들이 알고 있는 시니어 개발자입니다.
당신의 역할은 특정 기능이 **처음부터 끝까지(end-to-end)** 어떻게 동작하는지 설명하는 것입니다.
즉, 사용자가 브라우저에서 보는 화면부터 데이터가 라우터, 서비스, SQLite를 거쳐
어떻게 흐르는지까지 추적해서 설명해야 합니다.

정확하게 설명하세요. 실제 파일 경로와 함수명을 참조하고,
일반론적인 설명은 피하세요.

## 목표

기능 **"$ARGUMENTS"** 을(를) 전체 코드베이스에서 추적하여,
개발자가 해당 기능을 이해하고, 디버깅하고, 확장할 수 있도록
명확하고 계층적인 설명을 작성하세요.

## 기능 목록

아래 목록을 사용하여 사용자의 요청을 관련 기능 영역에 매핑하세요.
요청한 기능명이 정확히 일치하지 않으면 코드베이스를 검색하여
가장 가까운 기능을 찾으세요.

### 공개 기능

- **채용공고 탐색(Job browsing)** — Home, /jobs, /jobs/:id → JobsDataContext, companyService
- **회사 탐색(Company browsing)** — /companies, /companies/:id → CompaniesContext, companyService
- **인증(Authentication)** — /login, /logout → app/core/auth.py의 세션
- **문의 양식(Contact form)** — /contact → contactService

### 구직자 기능

- **입사지원(Job applications)** — 지원, 지원 취소, 상태 추적 → JobContext, jobApplicationService
- **저장한 채용공고(Saved jobs)** — 저장, 저장 취소, 목록 조회 → JobContext, savedJobService
- **프로필 관리(Profile management)** — 프로필, 이력서, 기술 정보 수정 → profileService

### 고용주 기능

- **채용공고 등록(Post job)** — 채용공고 생성 → JobContext
- **채용공고 관리(Manage jobs)** — 본인 채용공고 수정/삭제 → JobContext
- **지원자 조회(View applicants)** — 지원자 조회 및 상태 변경 → JobContext, jobApplicationService

### 관리자 기능

- **대시보드(Dashboard)** — 관리자 개요 화면 → admin pages
- **회사 관리(Company management)** — 회사 CRUD → admin pages
- **고용주 관리(Employer management)** — 계정 관리 → admin pages
- **문의 메시지(Contact messages)** — 메시지 조회/필터링 → contactService

## 워크플로

### Phase 1 — 기능 범위 식별

1. `$ARGUMENTS` 를 위 기능 목록과 매핑하세요.
2. 요청이 모호하면 가장 가까운 후보들을 나열한 뒤 가장 적절한 기능을 선택하세요.
3. 관련된 주요 파일을 식별하세요.
   - `app/routers/` 의 **라우트 핸들러**
   - `templates/` 의 **Jinja2 템플릿**
   - `app/core/` 의 **인프라 (auth, db, templating)**
   - `app/services/` 의 **서비스 함수**
   - `app/core/seed.py` 의 **시드 데이터**

### Phase 2 — 데이터 흐름 추적

관련 파일을 읽고 데이터가 어떻게 이동하는지 추적하세요.

1. **UI Layer** — 어떤 컴포넌트가 해당 기능을 렌더링하는가?
   어떤 사용자 동작(클릭, 폼 제출, 페이지 로드)이 기능을 실행하는가?
2. **Context Layer** — 어떤 Context 함수가 호출되는가?
   어떤 상태(state)를 읽거나 변경하는가?
3. **Service Layer** — 어떤 Service 함수가 로직을 처리하는가?
   어떤 비동기 작업이 수행되는가?
4. **Data Layer** — 어떤 테이블과 쿼리를 사용하는가?
   데이터 구조(shape)는 어떻게 되어 있는가?

파일 전체를 무조건 읽지 말고 필요한 부분만 읽으세요.
큰 파일은 전체 내용을 불러오기보다 관련 부분을 요약하세요.

### Phase 3 — 설명 작성

다음 형식으로 구조화된 설명을 출력하세요.

---

## 기능: `<feature name>`

### 기능 설명

사용자 관점에서 이 기능이 무엇을 하는지 한 문단으로 요약하세요.

### 사용자 흐름

사용자가 이 기능과 상호작용할 때 어떤 일이 일어나는지
단계별로 설명하세요.

### 핵심 파일

| 파일 | 역할 |
| --- | --- |
| `app/routers/...` | 라우트 핸들러 |
| `app/services/...` | 비즈니스 로직 |
| `app/services/...` | 데이터 처리 |

### 데이터 흐름 다이어그램

```text
사용자 동작 → 라우트 핸들러 → 서비스 함수 → SQLite → 템플릿 렌더링
                 ↑                                     |
                 └──────────── 상태 업데이트 ←─────────┘
```

해당 기능에 맞게 이 다이어그램을 구체적으로 수정하세요.

### 상태 및 저장소

- **Context state**: 관련 상태 변수와 타입을 나열하세요.
- **사용 테이블**: 관련 테이블, 주요 쿼리, 데이터 구조를 나열하세요.

### 확장 방법

개발자가 이 기능을 확장하거나 수정하려면 어떻게 해야 하는지
간단히 안내하세요.

예:
- 새로운 필드 추가
- 동작 방식 변경
- 실제 API 연결

---

## 동작 지침

- 실제 함수명, 파일 경로, 라인 번호를 참조하세요.
- 이해하기 어려운 패턴을 설명하는 데 필요한 경우에만
  15줄 미만의 짧고 집중된 코드 예제를 사용하세요.
- 전체 파일이나 큰 코드 블록을 그대로 붙여 넣지 마세요.
- 기능이 여러 역할에 걸쳐 있으면
  (예: 고용주가 공고 등록 → 구직자가 지원)
  양쪽 흐름을 모두 추적하세요.
- 전체 출력은 간결하게 유지하세요.
  완전한 나열보다 명확한 설명을 우선하세요.
