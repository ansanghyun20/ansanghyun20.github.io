---
layout: post
title: 백준 - 숫자 카드 (이분탐색2)
subtitle: 백준 숫자카드 문제 풀이 
categories: codingTest
tags: [codingTest]
---

# 백준 숫자카드 문제 풀이

https://www.acmicpc.net/problem/10816

### 입력

입력을 4가지를 받는다.

1. 첫 번째 배열의 길이
2. 첫 번째 배열
3. 두 번째 배열의 길이
4. 두 번째 배열

### 문제 이해

문제의 이해는 다음과 같다.

두 번째 배열에 각 원소가 첫 번째 배열에 몇개 존재하는지 하나씩 출력하는 문제이다.

첫 번째 시도는 이분 탐색을 응용해서 시도 하였는데 이분 탐색을 모두 끝까지 시도해 시간 초과 오류를 발생하였다.

따라서 lower 탐색, upper 탐색 방법을 사용해 문제를 해결할 수 있었고 해시를 사용해 쉽게 해결이 가능하였다.


# 1. 이분 탐색

일반 적인 이분 탐색은 값을 하나 찾는 것이다.

여기서 이분 탐색은 중복되는 수가 있을 경우 첫 자리와 끝 자리의 배열 번호를 리턴해주는 함수로 만든다.

각각 lowerSearch, upperSearch가 되겠다.

### lowerSearch

`if arr[mid]>=key:` 으로 key 값에 대해 arr[mid]값이 크거나 동일할 때 last를 mid로 바꿔주며 해당하는 중복된 번호의 첫 번째 숫자를 찾아간다.

예는 다음과 같다

1. 1 `1` `2` 2 2 2 `6` 6 8 8 8 10 10 10 이라는 숫자가 있다고 가정한다. (숫자 2를 탐색한다.)
2. lowerSearch는 이분 탐색을 통해 중간 값(6 -> 2 -> 1)을 찾아 나간다.
3. key값(2)이 탐색된 mid보다 작을 때 마다 last를 mid로 당겨온다.
4. key값(2)이 탐색된 mid보다 커지면 start를 mid+1로 중복된 2의 가장 앞자리 인덱스(2)를 가져온다. 
5. start와 last가 같아지면 while문을 종료 하는 방식이다.

### upperSearch

`if arr[mid]>key:` 으로 key 값에 대해 arr[mid]값이 클때 last를 mid로 바꿔주며 해당하는 중복된 번호의 초과하는 수를 찾아간다.

lowerSearch와 다른점은 부등호이다. 

부등호 하나로 찾고자 하는 값의 초과하는 값을 찾아갈 수 있다.

### 소스코드

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

# 2. 해시
