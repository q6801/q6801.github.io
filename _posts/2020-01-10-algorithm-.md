---
title: 최단 경로 알고리즘
---

## 최단 경로 문제
- 최단 경로 알고리즘은 가장 짧은 경로를 찾는 알고리즘을 의미한다.
- 각 지점은 그래프에서 노드로 표현
- 지점 간 연결된 도로는 그래프에서 간선으로 표현

## 다익스트라 최단 경로
- 특정한 노드에서 출발하여 다른 모든 노드로 가는 최단 경로를 계산한다.
- 다익스트라 알고리즘은 음의 간선이 없을 때 정상적으로 동작한다.
- 다익스트라 최단 경로 알고리즘은 그리디 알고리즘으로 분류된다.


## 다익스트라 알고리즘 특징
- 그리디 알고리즘 : **매 상황에서 방문하지 않은 가장 비용이 적은 노드를 선택** 해 임의의 과정을 반복한다.
- 단계를 거치며 <span style="color:red">한 번 처리된 노드의 최단 거리는 고정</span>되어 더이상 바뀌지 않는다.

```python
import sys
input = sys.stdin.readline
INF = 1e9
n, m = map(int, input().split())

start = int (input())

graph = [[] for _ in range(n+1)]
distance = [INF] * (n+1)
visited = [False] * (n+1)

for i in range(m):
  a, b, c = map(int, input().split())
  graph[a] = [b, c]

def get_smallest_node():
  min_value = INF
  idx = 0
  for i in range(1, n+1):
    if not visited[i] and distance[i] < min_value :
      min_value = distance[i]
      idx = i
  return idx

def dijkstra(start):
  visited[start] = True
  distance[start] = True
  for b, c in graph[start]:
    distance[b] = c
  
  for i in range(n-1):
    now = get_smallest_node()
    visited[now] = True
    for b, c in graph[now]:
      if distance[now] + c < distance[b]:
        distance[b] = distance[now] + c

dijkstra(start)
```
## 다익스트라 알고리즘 : 성능 분석
- 총 O(V)번에 걸쳐서 최단 거리가 가장 짧은 노드를 매번 선형 탐색(O(V))해야 한다.
- 따라서 전체 시간 복잡도는 O(V^2)이다.
- 일반적으로 코딩 테스트의 최단 경로 문제에서 전체 노드의 개수가 5000개 이하라면 이 코드로 문제를 해결할 수 있다.
- 그 이상의 노드의 개수를 처리하기 위해서는 우선순위 큐와 힙을 알아야한다.


## 우선순위 큐 (Priority Queue)
- 우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료구조이다.
- python, java를 포함한 대부분의 언어에서 표준 라이브러리 형태로 지원한다.


## 힙 (Heap)
- <span style="background-color:rgba(0, 250, 0, 0.4);">우선순위 큐를 구현하기 위해 사용하는 자료구조 중 하나</span>이다.
- 최소 힙과 최대 힙이 있다.
- 다익스트라 최단 경로 알고리즘을 포함해 다양한 알고리즘에서 사용된다.
- 삽입 시간과 삭제 시간이 O(logN)이다.
- 파이썬의 기본 라이브러리인 heapq를 사용하면 min heap으로 구현되어있다.

## 다익스트라 : 개선된 구현 방법
- 단계마다 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택하기 위해 힙 자료구조를 이용한다.
- 가장 짧은 노드를 선택하기 위해 최소 힙을 사용한다.
