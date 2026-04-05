---
title: "[BOJ] 14863 - 서울에서 경산까지"
date: 2026-04-06
draft: false
categories:
    - Algorithm
tags:
    - dp
    - knapsack
    - boj
    - gold-5
---

## 문제

서울에서 경산까지 N개의 구간을 이동하는데, 각 구간마다 도보 또는 자전거 중 하나를 선택할 수 있다. 각 선택에 따라 소요 시간과 모금액이 다르며, 전체 시간이 K분 이내일 때 모금액을 최대화하는 문제다.

- **제약 조건**: 3 ≤ N ≤ 100, K ≤ 100,000
- **링크**: [BOJ - 서울에서 경산까지](https://www.acmicpc.net/problem/14863)

## 핵심 포인트

- N이 최대 100, K가 최대 100,000이므로 일반적인 배낭 DP인 O(N × K)로 풀 수 있다.
- 각 구간에서 2가지 선택지(도보/자전거)가 있고, 시간 제한 내에서 모금액을 최대화해야 하므로 전형적인 배낭 문제 변형이다.
- 이 풀이는 표준 배낭 DP 대신 **파레토 최적 상태만 유지하는 방식**을 사용했다. `(시간, 모금액)` 쌍 중에서 시간이 더 적으면서 모금액도 더 적은 상태는 버린다(pruning). 시간 순 정렬 후 모금액이 단조증가하는 상태만 남기므로, 불필요한 탐색을 줄일 수 있다.
- 표준 O(N × K) 배열 DP에 비해 메모리 효율적이고, 실제 유효한 상태 수가 적으면 더 빠르게 동작한다.

## 풀이

```python
import sys
input = sys.stdin.readline

N, K = map(int, input().split())

stages = []
for _ in range(N):
  t1, s1, t2, s2 = map(int, input().split())
  stages.append(((t1, s1), (t2, s2)))


def prune(states, limit):
  max_sat = 0
  result = []
  for time, sat in states:
      if time > limit:
          break
      if sat > max_sat:
          max_sat = sat
          result.append((time, sat))
  return result


def combine(a, b):
  merged = [(at + bt, a_s + b_s) for at, a_s in a for bt, b_s in b]
  merged.sort()
  return merged


dp = [(0, 0)]
for stage in stages:
  dp = combine(dp, stage)
  dp = prune(dp, K)

print(dp[-1][1])
```

## 복잡도

- **시간**: 최악의 경우 O(N × K)이지만, pruning으로 유효 상태가 줄어들면 실질적으로 더 빠르다
- **공간**: O(유효 상태 수) — 표준 배낭 DP의 O(K)보다 효율적일 수 있다
