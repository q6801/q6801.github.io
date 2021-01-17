---
title: 이진 탐색
---

## 이진 탐색
- 정렬되어 있는 리스트에서 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하는 방법
- 단계마다 탐색 범위를 2로 나누는 것과 동일하므로 연산 횟수는 log2 N에 비례한다.
- 그래서 시간 복잡도는 O(log N)을 보장한다.

```python
array = [7, 5, 9, 0, 1]

def binary_search(array, target, start, end):
  if start >= end:
    return None
  mid = (start + end) // 2
  if array[mid] == target:
    return mid
  else:
    if array[mid] > target:
      return binary_search(array, target, start, mid-1)
    else:
      return binary_search(array, target, mid+1, end)

print(binary_search(array, 9, 0, len(array)-1))
```

## 파이썬 이진 탐색 라이브러리
- bisect_left(a, x) : 정렬된 순서를 유지하면서 배열 a에 x를 삽입할 가장 왼쪽 인덱스를 반환
- bisect_right(a, x) : 정렬된 순서를 유지하면서 배열 a에 x를 삽입할 가장 오른쪽 인덱스를 반환

```python
from bisect import bisect_left, bisect_right

a = [1, 2, 4, 4, 8]
x = 4

print(bisect_left(a, x))
print(bisect_right(a, x))

```
