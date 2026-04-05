---
name: blog-list
description: 블로그 글 목록 조회 / List all blog posts
---

# 블로그 글 목록 조회

## 목적
현재 블로그에 있는 모든 글의 목록을 보여준다.

## 블로그 경로
- 프로젝트 루트: `/Users/ijongmin/workspace/blog`
- 글 위치: `content/post/`

## 실행 흐름

### 1. 글 목록 수집
`content/post/` 하위의 모든 `index.md` 파일을 읽어서 front matter를 파싱한다.

### 2. 테이블로 출력
```
| # | 제목 | 날짜 | 카테고리 | 태그 | 상태 |
|---|------|------|----------|------|------|
| 1 | 블로그를 시작합니다 | 2026-04-05 | General | blog, hugo | 공개 |
| 2 | MySQL 락 가이드 | 2026-04-06 | Database | mysql, lock | draft |
```

### 3. 요약
```
전체: {N}개 | 공개: {X}개 | draft: {Y}개
```

## 필터링
인자가 전달되면 필터링한다:
- `/blog-list draft` → draft 글만
- `/blog-list Database` → 해당 카테고리 글만
- `/blog-list mysql` → 해당 태그 포함 글만
