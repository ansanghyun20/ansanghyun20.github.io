---
layout: post
title: 프로그래머스 - 기능 개발
subtitle: 프로그래머스 기능 개발 문제 풀이
categories: codingTest
tags: [codingTest]
---

1. 가장 먼저 날짜별로 필요한 일 수를 담는다 (lst 변수에).
2. lst[0] 보다 큰 값이 들어오면 lst를 비워준다. 그리고 answer에 값을 대입한다.
3. lst[0] 보다 작은 값이면 cnt를 증가 시켜준다.
4. 마지막으로 lst[0]보다 큰 값이 없어서 남은 cnt를 temp에 저장해서 추가해준다.

```python

import math
def solution(progresses, speeds):
    answer = []
    lst = []
    cnt = 1
    temp = 0

    for i in range(len(progresses)):
        perse = math.ceil((100-progresses[i]) / speeds[i])
        if len(lst)>0:
            if  lst[0] >= perse:
                cnt += 1
                
            else:
                answer.append(cnt)
                cnt = 1
                lst.clear()
            temp = cnt
        lst.append(perse)
        
    if temp != 0:
        answer.append(temp)
        
        
    return answer


```
