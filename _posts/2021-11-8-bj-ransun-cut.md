---
layout: post
title: 백준 - 랜선 자르기 (이분탐색3)
subtitle: 백준 랜선 자르기 문제 풀이 
categories: codingTest
tags: [codingTest]
---

### 백준 랜선 자르기 문제 풀이

https://www.acmicpc.net/problem/1654


### 문제풀이

#### 이해

이전에 했던 이분탐색 1과 이분탐색 2는 랜선 자르기와 같이 활용하는 문제를 위한 문제라고 할 수 있다.

주어진 배열을 입력받은 갯수 만큼 잘라 만드는 것이다.

#### 풀이 방식

아래의 소스코드의 풀이 방식은 다음과같다.

1. Upper 이분 탐색 트리를 이용한다.
2. `가장 큰 길이+1`을 last값으로 잡는다(0을 나누는 경우를 제외)
3. 중간 값의 이분 탐색을 진행하며 가장 큰 값을 찾기 때문에 upper 방식을 적용하는 것이다.
4. while문 안에 for문을 통해서 자르는 랜선의 갯수를 출력하고
5. 원하는 값보다 랜선의 갯수가 작으면 last 값을 mid로 가져오며 범위를 좁힌다.
6. 랜선의 갯수가 원하는 갯수보다 같거나 커졌을 때 start를 mid로 가져온다.

#### 소스코드

```python
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
    for i in B:          # 일반적인 upper 이분탐색에는 쓰지 않는 부분
        cnt  += i//mid    
        
    if cnt<A[1]:         # 위에서만든 for문을 통해 입력받은 값과 비교
        last = mid
    else:
        start = mid + 1  # 입력받은 수가 작거나 같아지면 start를 mid+1


print(start-1)           # upper은 1 초과한 수를 찾으므로 -1을 하면 정답!
```
