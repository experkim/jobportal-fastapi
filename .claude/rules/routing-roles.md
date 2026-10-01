---
paths:
  - "app/routers/**/*.py"
  - "app/core/auth.py"
  - "app/core/templating.py"
  - "main.py"
  - "templates/**/*.html"
---

# 라우팅 및 역할 규칙

## 역할 정의

총 3개의 역할이 있으며, 각 역할마다 접근할 수 있는 보호된 경로가 다릅니다.

| 역할 | 접근 가능한 경로 |
| --- | --- |
| `seeker` | `/profile`, `/applied`, `/saved`, 공고 지원·저장 POST |
| `employer` | `/employer/*` |
| `admin` | `/admin/*` |

## 라우트 보호

- 보호된 라우트는 핸들러 첫 줄에서 `require_role(user, "역할")`을 호출합니다 (`app/core/auth.py`).
- 현재 사용자는 `user=Depends(get_current_user)`로 주입받습니다. 비로그인 시 None입니다.
- 템플릿 렌더링은 `app/core/templating.py`의 `render()`를 사용해 user가 항상 주입되게 합니다.

## 라우팅 컨벤션

- 폼 제출(POST) 성공 후에는 항상 `RedirectResponse(..., status_code=303)`으로 리다이렉트합니다 (PRG 패턴).
- 새 라우터 파일은 `main.py`의 `include_router`에 등록해야 활성화됩니다.
- 역할별 내비게이션 링크는 `templates/partials/navbar.html`에서 조건 분기합니다.
