# Project Template

Claude Code 자율 개발 프로젝트 템플릿.

## 시작하기

1. **"Use this template"** 버튼으로 새 레포 생성
2. **Secrets 등록** (레포 Settings → Secrets → Actions):
   - `CLAUDE_CODE_OAUTH_TOKEN` — Organization Secrets에서 자동 상속 (이미 등록된 경우 스킵)
   - `GLOBAL_SETTINGS_TOKEN` — Organization Secrets에서 자동 상속
3. **CLAUDE.md 수정** — 프로젝트명, 스택, 고유 규칙 작성
4. **이슈 생성 + `@claude` 댓글** → 자동 실행

## 포함된 워크플로우

| 파일 | 용도 |
|---|---|
| `claude.yml` | @claude 댓글 → 즉시 실행 |
| `claude-code-review.yml` | PR 자동 리뷰 |
| `claude-dispatch.yml` | 수동 실행 + Paperclip dispatch |
| `ci-quality-gate.yml` | TypeScript/ESLint/테스트/커버리지 |
| `dependabot.yml` | 의존성 자동 업데이트 |

## 전역 설정

`my-claude-global` 레포의 CLAUDE.md가 전역 규칙으로 적용됩니다.
프로젝트 CLAUDE.md에는 프로젝트 특화 규칙만 작성하세요.
