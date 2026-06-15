# Project Template

Claude Code 자율 개발 프로젝트 템플릿. 새 프로젝트를 이 템플릿에서 생성하면 워크플로우가 자동으로 복사됩니다.

---

## 빠른 시작 (3단계)

### 1단계: 레포 생성
GitHub에서 이 레포의 **"Use this template"** 버튼 클릭 → 레포명 입력 → 생성

### 2단계: Secrets 등록

레포에서 Claude Code 터미널을 열고:
```
/install-github-app
```
→ `CLAUDE_CODE_OAUTH_TOKEN` 자동 등록

수동 등록 필요:
| Secret | 등록 위치 | 값 |
|---|---|---|
| `GLOBAL_SETTINGS_TOKEN` | 레포 Settings → Secrets → Actions | GitHub PAT (repo 스코프) |

### 3단계: CLAUDE.md 수정

```markdown
# 프로젝트 설정

## 프로젝트 정보
- 이름: [프로젝트명]
- 스택: [Next.js / React / Node.js 등]
- 패키지 매니저: pnpm

## 명령어
- `pnpm dev` — 개발 서버
- `pnpm build` — 빌드
- `pnpm test` — 테스트

## 프로젝트 고유 규칙
- [프로젝트 특화 규칙 작성]
```

---

## 작업 지시 방법

### 방법 1: GitHub 이슈 + @claude (즉시 실행)
이슈 또는 PR에 댓글:
```
@claude 로그인 기능 구현해줘
```

### 방법 2: 수동 디스패치 (Actions UI)
레포 **Actions → "Claude Code (수동 실행)" → Run workflow** 에서 `task` 입력:
```
[기능] 사용자 인증 API 구현
[정리] 미사용 import 제거
```

### 디스패치 흐름

```
task 입력 (workflow_dispatch / repository_dispatch)
  ↓ 작업 유형 자동 판단 (분석=opus / 정리=haiku / 일반=sonnet)
Claude 코드 수정 → claude/<id>-<timestamp> 브랜치 push
  ↓
PR 자동 생성 (검토 대기)
  ↓ 사람이 확인 후 머지  ← 머지는 사람 확인 게이트
완료
```

---

## 포함된 워크플로우

| 파일 | 트리거 | 역할 |
|---|---|---|
| `claude.yml` | `@claude` 댓글 | Claude Code 즉시 실행 |
| `claude-code-review.yml` | PR 생성/업데이트 | 자동 코드 리뷰 |
| `claude-dispatch.yml` | 수동 UI / `repository_dispatch` | 태스크 기반 실행 + PR 자동 생성 (머지는 사람 확인) |
| `ci-quality-gate.yml` | `src/`, `package.json` 변경 시 | TypeScript · ESLint · 테스트 · 커버리지 80% |
| `dependabot.yml` | 매주 월요일 KST 09:00 | npm · Actions 의존성 자동 업데이트 |

---

## 전역 설정

이 프로젝트의 `CLAUDE.md`는 **프로젝트 특화 규칙**만 담습니다.
공통 규칙은 [`my-claude-global`](https://github.com/hs85-newbie/my-claude-global) 레포에서 관리되며, Actions 실행 시 자동으로 로드됩니다.

```
우선순위:
1순위: ~/.claude/CLAUDE.md (전역, my-claude-global)
2순위: [프로젝트]/CLAUDE.md (프로젝트 특화, 이 파일)
```

---

## 브랜치 전략

- **dev**: 모든 코드 수정은 dev 브랜치에 반영
- **main**: 전체 점검 통과 후에만 dev → main 머지
- 디스패치 시 `branch` payload(또는 기본 `main`)로 대상 브랜치 지정

---

## 디렉토리 구조

```
project-template/
├── CLAUDE.md                          # 프로젝트 설정 (수정 필요)
├── README.md                          # 이 파일
├── .github/
│   ├── dependabot.yml                 # 의존성 자동 업데이트
│   └── workflows/
│       ├── claude.yml                 # @claude 댓글 트리거
│       ├── claude-code-review.yml     # PR 자동 리뷰
│       ├── claude-dispatch.yml        # 수동/dispatch 실행 + PR 생성
│       └── ci-quality-gate.yml        # CI 품질 게이트
```
