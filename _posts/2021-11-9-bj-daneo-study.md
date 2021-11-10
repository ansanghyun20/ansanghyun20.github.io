---
layout: post
title: 백준 - 단어 공부
subtitle: 백준 단어 공부 문제 풀이 
categories: codingTest
tags: [codingTest]
---

### 백준 단어 공부 답

https://www.acmicpc.net/problem/1157

### 소스코드
 
```python
A = input().upper()
A = list(A)
#print(A)
dic = {}
for i in A:
    try:
        dic[i] = dic[i]+1
    except:
        dic[i] = 1

max_ = 0
j = 0
cnt = 0
for i in dic:
    if max_ < dic[i]:
        max_ = dic[i]
        j = i
        
del dic[j]

for i in dic:
    if max_==dic[i]:
        cnt += 1
        print("?")
        break
    
if cnt==0:
    print(j)
```
