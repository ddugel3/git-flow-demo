# Git/GitHub 실무 협업 데모 발표 자료 (30분)

## Slide 1. 제목
- 제목: Git/GitHub 실무 협업 사이클 라이브 데모
- 부제: `Issue -> Branch -> Commit -> PR -> CI -> Review -> Merge -> Close Issue`

발표 멘트:
"오늘은 Git 명령어 나열이 아니라, 실무에서 실제로 한 일을 어떻게 흘려보내는지 30분 안에 한 바퀴 돌려보겠습니다."

---

## Slide 2. 오늘의 목표
- 기능 소개보다 "흐름" 이해
- 템플릿/규칙/자동화를 통한 품질 관리
- 머지와 이슈 종료까지 완결 경험

핵심 메시지:
- Git은 기록 도구
- GitHub는 협업 운영 도구

---

## Slide 3. 사전 세팅이 실무다
- `.github/ISSUE_TEMPLATE/bug_report.yml`
- `.github/pull_request_template.md`
- `.github/CODEOWNERS`
- `.github/workflows/ci.yml`
- `.gitignore`

발표 멘트:
"실무 팀은 코딩 전에 규칙을 먼저 고정합니다. 그래야 사람이 바뀌어도 품질이 유지됩니다."

---

## Slide 4. 이슈 템플릿
- 문제 설명
- 재현 방법
- 기대 동작

데모:
- GitHub에서 New Issue 클릭
- 템플릿이 뜨는 것 확인

포인트:
- "할 일"이 아니라 "검증 가능한 작업 단위"로 정의

---

## Slide 5. 브랜치 전략
- `main` 직접 작업 금지
- 이슈 번호 기반 브랜치 이름
- 예: `fix/12-login-button`

발표 멘트:
"브랜치 이름만 봐도 목적과 맥락이 읽혀야 협업 비용이 줄어듭니다."

---

## Slide 6. 커밋 규칙
- `feat: ...`
- `fix: ...`
- `docs: ...`

포인트:
- 커밋 메시지가 곧 변경 이력 문서

데모 명령:
```bash
git switch -c fix/12-login-button
git add .
git commit -m "fix: login button click handler"
```

---

## Slide 7. PR 생성과 자동 이슈 종료
- PR 본문에 `Fixes #12`
- Merge되면 Issue 자동 Close

데모:
- PR 생성 화면에서 템플릿 자동 삽입 확인

발표 멘트:
"PR은 코드 제출이 아니라 협업 요청입니다. 그래서 맥락(Why)이 반드시 필요합니다."

---

## Slide 8. CODEOWNERS와 리뷰
- `* @YOUR_GITHUB_ID`
- 파일/폴더 기준 리뷰 책임자 지정 가능

설명 포인트:
- 리뷰 누락 방지
- 책임 경계 명확화

---

## Slide 9. CI (GitHub Actions)
- 트리거: `pull_request` to `main`
- 검사: 금지 문자열 `error` 포함 여부

데모:
1. 정상 PR -> CI 성공
2. `error`를 일부러 넣고 push -> CI 실패
3. 수정 후 재푸시 -> CI 재성공

발표 멘트:
"CI는 서버에서 동일한 기준으로 검증하므로, 로컬 환경 차이를 줄여줍니다."

---

## Slide 10. Git Hook vs CI
- Hook: 로컬에서 빠른 차단
- CI: 서버에서 중앙 검증

예시:
- `pre-commit`으로 금지 문자열 차단

포인트:
- 둘 중 하나가 아니라 둘 다 필요

---

## Slide 11. .gitignore 실무 포인트 (macOS 포함)
- 내부 문서: `LECTURE_SCRIPT.md`
- macOS: `.DS_Store`, `._*`
- IDE: `.vscode/`, `.idea/`

발표 멘트:
"코드와 무관한 파일이 이력에 들어오면 협업 품질이 급격히 떨어집니다."

---

## Slide 12. 머지 전략
- Squash Merge 권장
- PR 단위로 히스토리 정리

설명:
- 기능/이슈 단위로 로그 가독성 확보

---

## Slide 13. worktree 긴급 대응
상황:
- feature 작업 중 hotfix 긴급 요청

데모 명령:
```bash
git worktree add ../hotfix -b hotfix
git worktree list
git worktree remove ../hotfix
```

포인트:
- 브랜치 전환 스트레스 없이 병렬 작업

---

## Slide 14. 오픈소스와 동일한 흐름
- `Fork -> Branch -> Commit -> PR -> Review -> Merge`

발표 멘트:
"오픈소스는 실무 협업 프로세스를 공개 환경에서 수행하는 버전입니다."

---

## Slide 15. 오늘 요약
- 협업은 이슈로 시작
- 품질은 템플릿 + 리뷰 + CI + Hook으로 유지
- 완료 기준은 머지가 아니라 Issue close까지

한 줄 마무리:
"좋은 개발자는 코드를 잘 짜는 사람을 넘어, 변경을 팀이 안전하게 흘리게 만드는 사람입니다."

---

## 부록 A. 라이브 데모 체크리스트
1. 레포 준비 상태 확인 (`main` 최신)
2. Issue 1개 생성
3. 브랜치 생성 후 수정/커밋/푸시
4. PR 생성 (`Fixes #번호`)
5. CI 성공/실패/재성공 시연
6. 리뷰 승인 시연
7. Squash Merge
8. Issue 자동 close 확인
9. worktree 시연

## 부록 B. 데모용 명령어 치트시트
```bash
# 브랜치 생성
git switch -c fix/12-login-button

# 수정 후 커밋
git add .
git commit -m "fix: login button click handler"

# 푸시
git push -u origin fix/12-login-button

# CI 실패 수정 후 재푸시
git add .
git commit -m "fix: remove forbidden text"
git push

# 머지 후 main 동기화
git switch main
git pull

# worktree 데모
git worktree add ../hotfix -b hotfix
git worktree list
git worktree remove ../hotfix
```
