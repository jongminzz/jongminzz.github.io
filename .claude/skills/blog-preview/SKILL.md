---
name: blog-preview
description: Hugo 블로그 로컬 미리보기 / Local preview of Hugo blog
---

# 블로그 로컬 미리보기

## 목적
Hugo 개발 서버를 실행하여 블로그를 로컬에서 미리 확인한다.

## 블로그 경로
- 프로젝트 루트: `/Users/ijongmin/workspace/blog`

## 실행 흐름

### 1. 기존 서버 확인
`lsof -i :1313`으로 이미 Hugo 서버가 실행 중인지 확인한다.

- 실행 중이면: "Hugo 서버가 이미 실행 중입니다. http://localhost:1313/ 에서 확인하세요." 출력
- 실행 중이 아니면: 서버를 시작한다

### 2. 서버 시작
```bash
cd /Users/ijongmin/workspace/blog && hugo server --port 1313 &
```

draft 글도 보고 싶다는 요청이 있으면:
```bash
cd /Users/ijongmin/workspace/blog && hugo server --port 1313 --buildDrafts &
```

### 3. 완료 메시지
```
Hugo 서버가 시작되었습니다!

URL: http://localhost:1313/
draft 포함: {예/아니오}

서버를 종료하려면 /blog-preview stop 을 입력하세요.
```

### 4. 서버 종료
`/blog-preview stop` 또는 "서버 종료" 요청 시:
```bash
pkill -f "hugo server"
```
