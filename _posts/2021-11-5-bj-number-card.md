---
layout: post
title: 백준 - 숫자 카드 (이분탐색2)
subtitle: 백준 숫자카드 문제 풀이 
categories: codingTest
tags: [codingTest]
---

# 백준 숫자카드 
ㅁㅜㄴㅈ
# 백준 숫자


## 1. 이분 탐색

```python

def lowerSearch(arr, key):
    start = 0
    last = M
    while(start<last):
        mid = (start+last)//2
        if arr[mid]>=key:
            last = mid
        else:
            start = mid + 1
    return start

def upperSearch(arr, key):
    start = 0
    last = M
    while(start<last):
        mid = (start+last)//2
        if arr[mid]>key:
            last = mid
        else:
            start = mid + 1
    return start

M = int(input())
A = list(map(int,input().split()))

M2 = int(input())
A2 = list(map(int,input().split()))

A.sort()

for i in A2:
    print(upperSearch(A,i)-lowerSearch(A, i), end=" ")




```

## 2. 해시
