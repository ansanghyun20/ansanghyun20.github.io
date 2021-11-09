---
layout: post
title: 백준 - 벌집 (수학)
subtitle: 백준 벌집 문제 풀이 
categories: codingTest
tags: [codingTest]
---

### 백준 벌집 문제 풀이

https://www.acmicpc.net/problem/2292

### 벌집

사이트에 접속하면 그림이 나온다. 거기서 임의의 수가 1과 얼마만큼 떨어져있는지 나타내는 문제! 입력은 임의의 수 이다.

#### 풀이 방식



아래의 코드는 다음과 같은 방식으로 풀었다.

1. 입력을 받는다.
2. 1부터 1, 7, 19, 37 으로 6의 배수 만큼 늘어난다.
3. 따라서 임의의 수보다 작은 6의 배수를 구한다.
4. 1일 때는 1을 출력!

#### 소스코드

A = int(input())
sumA = 1
i=1
while(1):
    #print(sumA)
    sumA += i*6
    i += 1
    if sumA>=A:
        break
if A == 1:
    print(1)
else:
    print(i)
