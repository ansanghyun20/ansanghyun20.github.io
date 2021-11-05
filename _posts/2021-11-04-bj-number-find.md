---
layout: post
title: 백준 - 수 찾기 (이분탐색1)
subtitle: 백준 수 찾기 문제 풀이 
categories: codingTest
tags: [codingTest]
---

### 백준 수 찾기 문제 풀이

https://www.acmicpc.net/problem/1920

#### 입력

입력을 4가지를 받는다.

1. 첫 번째 배열의 길이
2. 첫 번째 배열
3. 두 번째 배열의 길이
4. 두 번째 배열


#### 문제이해

문제는 간단하다. 두 번째 배열의 값이 첫 번째에 존재하는지 찾는다.

다만 for문에서 값을 검사하는 이분 탐색 알고리즘이 필요로 하다.

수행속도가 중요한 문제이다.


### 이분 탐색 이란?

이분 탐색은 중간 값을 계속 찾아나가며 범위를 좁혀 원하는 값을 찾아나가는 방식을 말한다.

1. 1 3 5 7 9 11 이라는 숫자가 있다고 가정해보자.
2. 3을 찾고싶다.
3. 먼저 배열의 중간 값인 5를 찾는다. (5를 제외한 뒷 배열들은 제외시킨다.)
4. 다음으로 중간 값인 3을 찾는다. (중간 값이 3과 일치하므로 찾을 수 있다.)

#### 소스코드

```python

def binarySearch(arr , key):
    l = int(N)-1
    s = 0
    while(s <= l):   
        mid = int((s+l)/2)
        if arr[mid] > key :
            l = mid -1
        elif arr[mid] < key:
            s = mid + 1
        else:
            return mid
        
N = int(input())
A = list(map(int, input().split()))
N2 = int(input())
A2 =  list(map(int, input().split()))
A.sort()
li = []
for i in range(len(A2)):
    if binarySearch(A, A2[i]) == None:
        print(0)
    else:
        print(1)

```
