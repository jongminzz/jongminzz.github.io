---
name: blog-publish
description: 블로그 변경사항 커밋 및 배포 / Commit and deploy blog changes
---

# 블로그 배포

## 목적
블로그의 변경사항을 git commit & push하여 GitHub Pages에 자동 배포한다.

## 블로그 경로
- 프로젝트 루트: `/Users/ijongmin/workspace/blog`
- 리모트: `https://github.com/jongminzz/jongminzz.github.io`

## Git 작성자 설정 (중요!)
커밋 시 반드시 아래 환경변수를 설정하여 개인 계정으로 커밋한다:
```
GIT_AUTHOR_NAME="jongminzz"
GIT_AUTHOR_EMAIL="jongminzzang97@gmail.com"
GIT_COMMITTER_NAME="jongminzz"
GIT_COMMITTER_EMAIL="jongminzzang97@gmail.com"
```

## 실행 흐름

### 1. 변경사항 확인
`git status`와 `git diff`로 변경사항을 확인한다.

변경사항이 없으면:
```
배포할 변경사항이 없습니다.
```

### 2. 변경 요약 표시
변경된 파일 목록과 요약을 사용자에게 보여준다:
```
변경사항:
- 새 글: content/post/mysql-lock-guide/index.md
- 수정: config/_default/params.toml

배포를 진행할까요?
```

### 3. 커밋 메시지 자동 생성
변경 내용에 따라 적절한 커밋 메시지를 생성한다:
- 새 글 추가: `Add post: {글 제목}`
- 글 수정: `Update post: {글 제목}`
- 설정 변경: `Update blog config`
- 여러 변경: `Update blog: {간단 요약}`

### 4. 커밋 및 푸시
사용자 확인 후 실행:
```bash
cd /Users/ijongmin/workspace/blog
git add .
GIT_AUTHOR_NAME="jongminzz" GIT_AUTHOR_EMAIL="jongminzzang97@gmail.com" \
GIT_COMMITTER_NAME="jongminzz" GIT_COMMITTER_EMAIL="jongminzzang97@gmail.com" \
git commit -m "{커밋 메시지}"
git push
```

### 5. 배포 확인
push 후 GitHub Actions 상태를 확인한다:
```bash
gh run list --repo jongminzz/jongminzz.github.io --limit 1
```

### 6. 완료 메시지
```
배포가 시작되었습니다!

커밋: {커밋 메시지}
GitHub Actions: {실행 중/완료}
블로그 URL: https://jongminzz.github.io

Actions 완료 후 블로그에서 확인할 수 있습니다.
```
