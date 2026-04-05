---
name: blog-new
description: Hugo 블로그 새 글 생성 / Create new Hugo blog post
---

# 새 블로그 글 생성

## 목적
Hugo 블로그에 새 글을 생성한다. 제목, 카테고리, 태그를 받아서 올바른 디렉토리 구조와 front matter를 갖춘 마크다운 파일을 만든다.

## 블로그 경로
- 프로젝트 루트: `/Users/ijongmin/workspace/blog`
- 글 저장 위치: `content/post/{slug}/index.md`

## 실행 흐름

### 1. 정보 수집
사용자에게 아래 정보를 대화로 수집한다:
- **제목** (필수): 글 제목
- **카테고리** (선택): 분류 (예: Backend, Frontend, DevOps, Database 등)
- **태그** (선택): 키워드들 (예: mysql, docker, kubernetes)
- **draft 여부** (선택, 기본값: false)

인자가 이미 전달된 경우 해당 질문은 건너뛴다.
예: `/blog-new MySQL 락 이해하기` → 제목은 이미 있으므로 카테고리/태그만 물어본다.

### 2. slug 생성
- 제목에서 영문 kebab-case slug를 생성한다
- 한글 제목이면 영문으로 의역한다
- 예: "MySQL 락 이해하기" → `mysql-lock-guide`
- 예: "Docker 컨테이너 네트워킹" → `docker-container-networking`

### 3. 파일 생성
`content/post/{slug}/index.md` 파일을 생성한다.

```markdown
---
title: "{제목}"
date: {오늘 날짜 YYYY-MM-DD}
draft: {draft 여부}
categories:
    - {카테고리}
tags:
    - {태그1}
    - {태그2}
---

여기에 글을 작성하세요.
```

### 4. 완료 메시지
```
새 글이 생성되었습니다!

파일: content/post/{slug}/index.md
제목: {제목}
카테고리: {카테고리}
태그: {태그들}

글을 작성한 후 /blog-preview로 미리보기, /blog-publish로 배포할 수 있습니다.
```
