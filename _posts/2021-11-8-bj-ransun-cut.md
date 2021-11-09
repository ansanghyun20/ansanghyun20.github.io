---
layout: post
title: 백준 - 랜선 자르기 (이분탐색3)
subtitle: 백준 랜선 자르기 문제 풀이 
categories: codingTest
tags: [codingTest]
---

### 백준 랜선 자르기 문제 풀이

https://www.acmicpc.net/problem/1654


###

A = list(map(int,input().split(" ")))
B = []
for i in range(A[0]):
    inp = int(input())
    B.append(inp)

start = 0
last = max(B)+1

while(start<last):
    mid = (start+last)//2
    cnt = 0
    for i in B:
        cnt  += i//mid    
    if cnt<A[1]:
        last = mid
    else:
        start = mid + 1


print(start-1)
