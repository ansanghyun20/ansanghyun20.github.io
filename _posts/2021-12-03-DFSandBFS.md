---
layout: post
title: 백준 - DFS와 BFS (DFS, BFS)
subtitle: 백준 DFS와 BFS 문제 풀이
categories: codingTest
tags: [codingTest]
---

### 백준 DFS와 BFS

<img width="1153" alt="image" src="https://user-images.githubusercontent.com/62547169/144698733-f6f061a4-ab76-4ba6-83a9-83b3dc241ac4.png">



### 소스코드
 
#### 해결 아이디어

- 
- 
- 

```python

# BFS
from collections import deque

def BFS(graph, root):
    visited = []
    queue = deque([root])

    while queue:
        n = queue.popleft()
        if n not in visited:
            visited.append(n)
            if n in graph:
                temp = list(set(graph[n]) - set(visited))
                temp.sort()
                queue += temp
    return " ".join(str(i) for i in visited)
  



#DFS
def DFS(graph, root):
    visited = []
    stack = [root]

    while stack:
        
        n = stack.pop()
        if n not in visited:
            visited.append(n)
            if n in graph:
                temp = list(set(graph[n]) - set(visited))
                temp.sort(reverse=True)
                stack += temp
            
    return " ".join(str(i) for i in visited)


graph = {}

node, line, root = map(int,input().split())

# 그래프 만들기 (양방향 그래프라서 a와 b에 둘다 넣는다.)
for i in range(0,line):
    a, b = map(int, input().split())
    try:
        graph[a].append(b)
    except:
        graph[a] = [b]

    try:
        graph[b].append(a)
    except:
        graph[b] = [a]

# 아무 것도 없을 때 빈 리스트 
for i in range(1,line):
    try:
        if graph[i] == None:
            pass
    except:
        graph[i] = []



print(DFS(graph, root))
print(BFS(graph, root))


```



