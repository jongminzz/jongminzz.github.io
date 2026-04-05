---
name: blog-import
description: 기존 마크다운 글을 Hugo 블로그로 가져오기 / Import existing markdown posts
---

# 기존 글 가져오기

## 목적
`~/workspace/posting/` 에 있는 기존 마크다운 파일을 Hugo 블로그 형식으로 변환하여 가져온다.

## 경로
- 원본: `/Users/ijongmin/workspace/posting/`
- 대상: `/Users/ijongmin/workspace/blog/content/post/{slug}/index.md`

## 실행 흐름

### 1. 원본 파일 목록 표시
`~/workspace/posting/*.md` 파일 목록을 보여준다:
```
가져올 수 있는 글 목록:

| # | 파일명 | 제목 (추정) |
|---|--------|------------|
| 1 | 2026-01-31-mysql-lock-complete-guide.md | MySQL 락 완벽 가이드 |
| 2 | 2026-02-01-http-version-history.md | HTTP 버전 히스토리 |
| ...

어떤 글을 가져올까요? (번호, 파일명, 또는 "전체")
```

### 2. 파일 분석
선택된 파일을 읽어서:
- 기존 front matter가 있으면 파싱
- 없으면 파일명과 내용에서 추정 (날짜, 제목)
- 파일명 패턴: `YYYY-MM-DD-{title}.md`

### 3. 변환 미리보기
Hugo 형식으로 변환한 결과를 미리 보여준다:
```
변환 미리보기:

원본: 2026-01-31-mysql-lock-complete-guide.md
대상: content/post/mysql-lock-complete-guide/index.md

front matter:
---
title: "MySQL 락 완벽 가이드"
date: 2026-01-31
draft: false
categories:
    - Database
tags:
    - mysql
    - lock
---

카테고리와 태그를 수정하시겠어요?
```

### 4. 카테고리/태그 확인
사용자에게 카테고리와 태그를 확인받는다.
- 내용을 분석하여 적절한 카테고리/태그를 제안
- 사용자가 수정 가능

### 5. 파일 생성
`content/post/{slug}/index.md`에 변환된 파일을 저장한다.

### 6. 완료 메시지
```
가져오기 완료!

{파일명} → content/post/{slug}/index.md

/blog-list로 목록을 확인하거나, /blog-preview로 미리보기할 수 있습니다.
```

## 주의사항
- 원본 파일은 수정하지 않는다 (복사만)
- 이미 같은 slug의 글이 있으면 덮어쓸지 확인한다
- 이미지가 포함된 경우 같은 디렉토리에 복사한다
