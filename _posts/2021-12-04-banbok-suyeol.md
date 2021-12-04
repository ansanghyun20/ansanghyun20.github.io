---
layout: post
title: 백준 - 반복수열
subtitle: 백준 반복수열 문제 풀이
categories: codingTest
tags: [codingTest]
---

### 백준 반복수열

<img width="1154" alt="image" src="https://user-images.githubusercontent.com/62547169/144698375-e7ed595e-d7fb-44ed-abb7-9a9c2aced194.png">


### 소스코드
 
#### 아이디어를 통한 문제 해결

1. list를 하나 만든다.
2. 새로운 숫자를 하나씩 만들면서, list에 추가한다.
3. list에 이미 존재하는 수에 새로운 수가 존재하면 이미 존재하는 수 뒤로 제거한다.
4. 이미 존재하던 list의 새로운 값의 index를 출력한다.


```python

a, n = map(str,input().split())

lst = [int(a)]  # 초기 list 설정
a = list(map(int,str(lst[0]))) # 계산을 하기 위해 분리 ex) [5,7]
length = len(str(lst[0]))   # 57일 경우 길이 2
while(1):
    
    new = 0
    for i in range(int(length)):    # 다음 수 계산
        new += a[i]**int(n)
        
    a = list(map(int,str(new)))     # 다음 수의 계산을 위한 분리
    length = len(a)                 # 길이
    
    if new in lst:                  # 기존에 list에 새로운 값이 존재하면
        print(lst.index(new))       # 기존 list에 새로운 값의 index 출력
        break
    else:
        lst.append(new)


```








