---
layout: post
title: 프로그래머스 기능 개발
subtitle: 인공지능
categories: CodingTest
tags: [CodingTest]
---

### 프로그래머스 - 기능개발

- 주먹구구식 해결
- 아래의 주석을 참고하면서 이해할 수 있다.


1. progresses의 길이가 1이면 코드를 돌릴필요 없는 코드 포함
2. 큰 수가 발견되기까지 누적



```python 

import math
def solution(progresses, speeds):
    answer = []
    p_r = []          # p_r에 각 progresses마다 걸리는 시간에 담기
    c=0
    for i in range(len(progresses)):
        c=(100-progresses[i])/speeds[i]
        p_r.append(math.ceil(c))  # 올림으로 담기
    print(p_r)
    result = []
    start=0
    z=p_r[0]
    tf=0
    if len(p_r)==1:                 # 길이가 하나일 때
        result.append(p_r[0])
        tf=1
    print(result)
    
    for j in range(len(p_r)):
        count=0
        
        if tf==1:       # progressr가 하나이면 이 코드를 돌릴 필요가 없음
            break
        
        for i in range(start,len(p_r)-1):
            count +=1
            if len(p_r)>1 and z<p_r[i+1]: #길이가 2부터 / 만약 더 큰수가 발견 됐다면
                result.append(count)
                start=i+1             # 위치 찾기(i+1)부터 
                z=p_r[i+1]
                break 
    if tf==0:       # 마지막에는 z<p_r[i+1] 부분이 발견되지 않으니까 남은 갯수 추가해주기
        result.append(len(p_r)-start)

    return result
    
```
