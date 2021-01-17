---
title: DFS/BFS
---

## DFS/BFS
- 탐색이란 많은 양의 데이터 중에원하는 데이터를 찾는 과정을 말한다.
- 대표적인 그래프 탐색 알고리즘으로 DFS와 BFS가 있다

## DFS (depth first search)
- dfs는 깊이 우선 탐색이라고도 부르며 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘이다.
-  <span style="background-color:rgba(0, 250, 0, 0.4);">스택 자료구조(혹은 재귀 함수)</span>를 이용한다.


```python
def dfs(graph, v, visited):
  visited[v] = True #현재 노드 방문 처리

  for i in graph[v]:
    if not visited[i]:
      dfs(graph, i, visited)
```


## BFS (Breadth First Search)
- BFS는 너비 우선 탐색이라고도 불리며, 그래프에서 가까운 노드부터 우선적으로 탐색하는 알고리즘
- BFS는 <span style="background-color:rgba(0, 250, 0, 0.4);">큐 자료구조를 이용한다.</span>

```python
from collections import deque

def bfs(graph, start, visited):
  queue = deque([start])
  # queue 구현을 위해 deque 라이브러리 사용
  visited[start] = True
  while queue:
    # 큐가 빌 때까지 반복
    v = queue.popleft()
    for i in graph[v]:
      if not visited[i]:
        queue.append(i)
        visited[i] = True

```
