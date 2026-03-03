# Git/GitHub 실무 데모 강의 스크립트 (30분)

## 0~3분: 오프닝
- 오늘 목표: 기능 설명이 아니라 실무 개발 사이클 1회전
- 한 줄 흐름: `Issue -> Branch -> Commit -> PR -> CI -> Review -> Merge -> Close Issue`

멘트 예시:
"Git은 버전 관리 도구, GitHub는 협업 관리 시스템입니다. 오늘은 이 한 사이클을 실제로 돌려보겠습니다."

## 3~6분: 규칙 세팅(실무는 규칙부터)
- 이슈 템플릿: 문제 설명/재현 방법/기대 동작 강제
- PR 템플릿: What/Why/How/Test/Issue 고정
- CODEOWNERS: 리뷰어 자동 지정
- CI: PR마다 자동 검사

멘트 예시:
"실무에서는 코딩보다 먼저 팀 규칙을 고정합니다. 템플릿과 자동화가 있어야 품질이 흔들리지 않습니다."

## 6~18분: 핵심 데모 사이클
1. 이슈 생성
- 제목: `[Bug] 로그인 버튼 동작 안 함`
- 내용: 문제 설명/재현 방법/기대 동작 작성

멘트:
"실무에서 작업은 대부분 이슈로 시작합니다."

2. 이슈 기반 브랜치 생성
- 브랜치명: `fix/12-login-button`

멘트:
"main에서 직접 작업하지 않고, 목적이 분명한 브랜치에서 작업합니다."

3. 수정 후 커밋/푸시
- 커밋: `fix: login button click handler`

4. PR 생성
- 본문에 `Fixes #12` 포함

멘트:
"`Fixes #번호`를 쓰면 머지 시 이슈가 자동으로 닫힙니다."

5. CI 확인
- Actions 탭에서 자동 실행 확인
- 실패 1회 의도적으로 시연 후 수정/재푸시

멘트:
"PR은 코드 공유가 아니라 자동 검증 파이프라인의 시작점입니다."

6. 리뷰/머지
- CODEOWNERS로 리뷰어 자동 지정 확인
- 승인 후 Squash Merge
- 이슈 자동 close 확인

## 18~23분: Git Hook
- 로컬 검사: Hook
- 서버 검사: CI

pre-commit 예시:
- 금지 문자열(`error`) 발견 시 커밋 차단

멘트:
"Hook으로 빠르게 막고, CI로 중앙에서 다시 검증합니다."

## 23~27분: worktree
상황:
- feature 작업 중 긴급 hotfix 요청

명령어:
```bash
git worktree add ../hotfix -b hotfix
git worktree list
```

설명:
- 폴더 2개에서 동시에 작업 가능
- 컨텍스트 전환 비용 감소

정리 명령어:
```bash
git worktree remove ../hotfix
```

## 27~30분: 오픈소스 연결
- 내부 실무와 동일한 흐름
- `Fork -> Branch -> PR -> Review -> Merge`

멘트:
"오픈소스는 실무 협업을 공개 환경에서 수행하는 형태입니다."

## 데모용 커맨드 치트시트
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

# 머지 후 동기화
git switch main
git pull

# worktree 데모
git worktree add ../hotfix -b hotfix
git worktree list
git worktree remove ../hotfix
```
