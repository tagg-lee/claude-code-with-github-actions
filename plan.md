# GitHub Actions + Claude Code 설치 계획

> 참고 레포: https://github.com/joonlab/claude-code-with-github-actions

---

## 목표

GitHub Actions를 활용해 Claude Code를 서버리스로 실행.
Mini PC, VPS 없이 GitHub 무료 인프라로 AI 자동화 워크플로우 구축.

---

## 사전 준비

- [ ] GitHub 계정 (이미 있음)
- [ ] Claude Max 구독 또는 Anthropic API Key
- [ ] Claude Code CLI 로컬 설치 확인

---

## 단계별 실행 계획

### Phase 0: 레포 Fork 및 기본 설정

1. https://github.com/joonlab/claude-code-with-github-actions 를 Fork
2. Fork한 레포를 로컬에 clone (이 프로젝트 폴더 또는 별도 폴더)
3. `.github/workflows/` 폴더 구조 확인

### Phase 1: OAuth 토큰 발급 및 Secret 등록

1. 로컬에서 Claude Code CLI 실행
2. `/login` 명령어로 OAuth 로그인
3. 발급된 `CLAUDE_CODE_OAUTH_TOKEN` 복사
4. GitHub 레포 > Settings > Secrets and variables > Actions
5. `CLAUDE_CODE_OAUTH_TOKEN` 이름으로 Secret 등록

### Phase 2: Step 1 - Hello Claude 테스트

**파일:** `.github/workflows/step1-hello-claude.yml`

- Actions 탭에서 workflow 수동 트리거
- Claude Code가 GitHub Actions 환경에서 실행되는지 확인
- 성공 여부 로그 확인

### Phase 3: Step 2 - 스케줄 자동화

**파일:** `.github/workflows/step2-scheduled.yml`

- cron 문법으로 주기적 실행 설정
- 결과를 git commit으로 레포에 저장하는 패턴 확인
- 스케줄 테스트 (수동 트리거로 먼저 확인)

### Phase 4: Step 3 - MCP 서버 연동

**파일:** `.github/workflows/step3-with-mcp.yml`

- Chrome DevTools 프로토콜 기반 웹 자동화
- MCP 서버 설정 방법 학습
- 실제 웹 크롤링 또는 브라우저 작업 테스트

### Phase 5: Step 4 - Full Pipeline

**파일:** `.github/workflows/step4-full-pipeline.yml`

- Skills + Subagents 패턴 적용
- 뉴스 다이제스트, 레포 헬스체크 등 실용 예제 실행
- 커스텀 워크플로우로 확장 계획 수립

---

## 비용 구조

| 항목 | 내용 |
|------|------|
| GitHub Actions | private 레포: 월 2,000분 무료 / public 레포: 무제한 |
| Claude API | Claude Max 구독 시 OAuth 토큰으로 사용 가능 |
| 인프라 | $0 (서버 불필요) |

---

## 주의사항

- GitHub Actions 무료 티어 한도 초과 시 과금 발생 가능 → **public 레포로 진행 권장**
- OAuth 토큰은 절대 코드에 하드코딩 금지 → GitHub Secrets만 사용
- 워크플로우 내 파일 출력은 `output/` 폴더 지정 권장

---

## 예상 활용 시나리오

- 매일 아침 뉴스/RSS 요약 → Obsidian 노트로 자동 저장
- 레포 코드 품질 자동 리뷰 (PR 생성 시 트리거)
- 정기적인 데이터 수집 및 분석 리포트 생성
- CMDS 세미나 관련 콘텐츠 자동화

---

## 다음 액션

1. 레포 Fork
2. OAuth 토큰 발급
3. Step 1 Hello 테스트 실행
