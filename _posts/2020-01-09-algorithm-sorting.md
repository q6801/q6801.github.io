---
title: 정렬 알고리즘
---

## 정렬 알고리즘
- 정렬이란 데이터를 특정한 기준에 따라 순서대로 나열하는 것
- 일반적으로 문제 상황에 따라서 적절한 정렬 알고리즘이 공식처럼 사용된다.


## 선택 정렬
- 처리되지 않은 데이터 중에서 <span style="background-color:rgba(0, 250, 0, 0.4);">가장 작은 데이터를 선택해 맨 앞에 있는 데이터와 바꾸는 것을 반복</span>한다.
- O(n^2)의 시간 복잡도가 소요된다.

```python
array = [7, 5, 9, 0, 1]

for i in range(len(array)):
  min_index = i # 가장 작은 원소의 인덱스
  for j in range(i+1, len(array)):
    if array[min_index] > array[j]:
      min_index = j
  array[i], array[min_index] = array[min_index], array[i]

print(array)
```

## 삽입 정렬
- 처리되지 않은 데이터를 하나씩 골라 적절한 위치에 삽입한다.
- 선택 정렬에 비해 구현 난이도가 높은 편이지만, 일반적으로 더 효율적으로 동작한다.
- 시간 복잡도는 O(n^2)이며, 선택 정렬과 마찬가지로 반복문이 두 번 중첩되어 사용된다.
- 하지만 삽입 정렬은  <span style="background-color:rgba(0, 250, 0, 0.4);">현재 리스트의 데이터가 거의 정렬되어 있는 상태라면 매우 빠르게 동작한다.</span>

```python
array = [7, 5, 9, 0, 1]

for i in range(1, len(array)):
  for j in range(i, 0, -1):
  # 원하는 위치에 삽입을 위해서 하나씩 옮긴다.
    if array[j] < array[j-1]:
      array[j], array[j-1] = array[j-1], array[j]
    else:
      break
```

## 퀵 정렬
- 기준 데이터(pivot)을 설정하고 그 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 방법이다.
- 병합 정렬과 더불어 대부분의 프로그래밍 언어의 정렬 라이브러리의 근간이 되는 알고리즘이다.
- 평균의 경우 O(N logN)의 시간 복잡도를 가지지만 최악의 경우 O(N^2)의 시간 복잡도를 가진다.

```python
array = [7, 5, 9, 0, 1]

def quick_sort(array, start, end):
  if start >= end: # 원소가 하나일 때 종료 조건으로 없으면 무한 재귀에 빠짐
    return
  pivot = start # 피벗은 첫 원소
  left = start + 1
  right = end

  while (left <= right):
    while left <= end and array[left] <= array[pivot]:
      left += 1
    while right > start and array[right] >= array[pivot]:
      right -= 1
    
    if left > right:
      array[pivot], array[right] = array[right], array[pivot]
    else:
      array[left], array[right] = array[right], array[left]
  quick_sort(array, start, right-1)
  quick_sort(array, right+1, end)

quick_sort(array, 0, len(array)-1)
print(array)

```
- 혹은 파이썬의 장점을 활용하면 아래와 같이 표현 가능하다.

```python
array = [7, 5, 9, 0, 1]

def quick_sort(array):
  if len(array) <= 1:
    return array
  pivot = array[0]
  tail = array[1:]

  left_side = [x for x in tail if x  <= pivot]
  right_side = [x for x in tail if x  > pivot]

  return quick_sort(left_side) + [pivot] + quick_sort(right_side)

print(quick_sort(array))

```

## 계수 정렬
- 특정한 조건이 부합할 때만 사용할 수 있지만 매우 빠르게 동작하는 정렬 알고리즘이다.
- <span style="background-color:rgba(0, 250, 0, 0.4);">데이터 크기 범위가 제한되어 정수 형태로 표현할 수 있을 때</span> 사용 가능하다.
- 데이터의 개수가 N, 데이터 중 최대값이 K일 때 최악의 경우에도 수행 시간 O(N+K)를 보장한다.
- 계수 정렬은 때에 따라서 심각한 비효율성을 초래할 수 있다.
- **동일한 값을 가지는 데이터가 여러 개 등장** 할 때 효과적으로 사용 가능하다.

```python
array = [7, 5, 9, 0, 1]

count = [0] * (max(array)+1)

for i in array:
  count[i] += 1 # 각 데이터에 해당하는 인덱스의 값 증가

for i in range(len(count)):
  for j in range(count[i]):
    print(i)
  
```
