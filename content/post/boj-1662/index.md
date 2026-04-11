---
title: "[BOJ] 1662 - 압축"
date: 2026-04-11
draft: false
categories:
    - Algorithm
tags:
    - stack
    - recursion
    - boj
    - gold-5
---

## 문제

압축된 문자열 S가 주어진다. `K(Q)` 형태는 문자열 Q를 K번 반복한다는 뜻이며, 괄호는 중첩될 수 있다. 압축을 풀었을 때 문자열의 길이를 구하는 문제다.

- **제약 조건**: S 길이 ≤ 50, 결과 ≤ 2,147,473,647
- **링크**: [BOJ - 압축](https://www.acmicpc.net/problem/1662)

## 핵심 포인트

- 괄호가 등장하는 문자열 처리는 **스택** 또는 **재귀**로 접근하는 것이 정석이다.
- S 길이가 최대 50이므로 시간복잡도 제약은 거의 없지만, 압축을 풀면 결과가 최대 약 21억이므로 **실제 문자열을 만들면 안 된다**. 길이만 추적해야 한다.
- 스택에 문자(str)와 계산된 길이(int)를 함께 넣을 때, `isinstance(p, int)`로 타입을 구분하면 문자열 태깅 없이 깔끔하게 처리할 수 있다.

## 풀이 1: 스택 + 문자열 태깅

```python
from collections import deque

d = deque()
l = input()

for x in l:
    if x == ')':
        t = 0
        while True:
            p = d.pop()
            if p == '(':
                mult = d.pop()
                d.append("len " + str(int(mult)*t))
                break
            if "len" in p:
                t += int(p[4:])
            else:
                t += 1
    else:
        d.append(x)

answer = 0
for x in d:
    if "len" in x:
        answer += int(x[4:])
    else :
        answer += 1

print(answer)
```

`)`를 만나면 `(`까지 pop하면서 내부 길이를 계산하고, `"len N"` 형태의 문자열로 다시 push한다. 직관적이지만 매번 문자열 생성과 파싱이 필요하다.

## 풀이 2: 스택 + isinstance

```python
import sys

def main():
    l = sys.stdin.readline().strip()
    d = []

    for x in l:
        if x == ')':
            t = 0
            while True:
                p = d.pop()
                if p == '(':
                    mult = int(d.pop())
                    d.append(mult * t)
                    break
                t += p if isinstance(p, int) else 1
        else:
            d.append(x)

    answer = sum(p if isinstance(p, int) else 1 for p in d)
    print(answer)

main()
```

핵심 변경점:
- **`deque` → `list`**: 스택 용도로는 `list`가 더 빠르다. `deque`의 양방향 기능이 불필요하다.
- **문자열 태깅 제거**: 계산된 길이를 `int`로 직접 push한다. `isinstance(p, int)`로 문자와 길이 값을 구분하면 문자열 검색/슬라이싱/파싱이 전부 사라진다.
- **`sum()` 제너레이터**: 마지막 집계를 한 줄로 처리한다.

## 별해: 재귀 하강 파서

스택 대신 재귀만으로도 풀 수 있다. 인덱스를 전진시키며 `(`를 만나면 재귀 호출, `)`를 만나면 반환하는 방식이다.

```python
def solve():
    s = input()
    idx = 0

    def parse():
        nonlocal idx
        length = 0
        while idx < len(s) and s[idx] != ')':
            if idx + 1 < len(s) and s[idx + 1] == '(':
                k = int(s[idx])
                idx += 2
                inner = parse()
                idx += 1
                length += k * inner
            else:
                length += 1
                idx += 1
        return length

    print(parse())

solve()
```

괄호의 중첩 구조가 곧 재귀 구조이므로, 재귀 하강 파서가 자연스럽게 들어맞는다. 스택을 명시적으로 관리할 필요가 없어 코드가 간결하다.

## 복잡도

- **시간**: O(N) — 각 문자를 한 번씩 처리
- **공간**: O(N) — 스택 크기 또는 재귀 깊이
