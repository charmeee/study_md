
all any
```python
from collections import deque
import heapq
heap = []
heapq.heappush(heap, 50)
heapq.heapify(heap2)
result = heapq.heappop(heap)
import math
```
find 문자열 없어도 에러안나고 -1 뜸
index 없으면 에러남 
### 회전
- 시계방향 90도
```python
list(map(list, zip(*array [: : -1 ])))
```
- 반시계방향 90도
```python
 list(map(list, zip(*array)))[: :-1]
```

### set
```python
s1 = set([1, 2, 3])
l1 = list(s1)
# 추가
s1.add(4)
# 여러개 추가
s1.update([4, 5, 6])
# 값 제거
s1.remove(2)
```
교집합 & ,차집합 - , 합집합 |
for문돌릴수는잇음

### 큐
```python
from collections import deque
queue = deque([4, 5, 6])
```

### heapq
```python
import heapq 
heap = [] 
heapq.heappush(heap, 50) 
heap2 = [50 ,10, 20] heapq.heapify(heap2)
result = heapq.heappop(heap)
```

### join
조인할때 대상이 str 인지확인해야함
안그러면조인안됨.
```python
ans+=(' '.join(map(str,switches[start:end])))
```

### 타입체크
```python
if isinstance(x, int):
```

### dictionary
```python
for key, value in {'a': 10, 'b': 20, 'c': 30, 'd': 40}.items():
    print(key, value)
```
## 배열
파이썬에서 원본 배열(리스트)을 자르려면 슬라이싱 결과를 **원본 리스트에 다시 할당**하거나, **리스트의 일부를 삭제**하는 방법을 사용할 수 있습니다. 슬라이싱은 기본적으로 새로운 리스트를 반환하므로, 이를 원본에 반영하려면 명시적으로 수정해야 합니다.

### 이차원배열
    list =[[0]*m for _ in range(n)]

### 원본 리스트를 직접 자르는 방법들:

1. **슬라이싱 후 원본 리스트에 다시 할당하기**

```python
arr = [1, 2, 3, 4, 5]

# 원본 리스트를 인덱스 1부터 3까지로 잘라서 다시 할당
arr = arr[1:3]
print(arr)  # 출력: [2, 3]
```

2. **`del` , 슬라이싱을 사용해 리스트의 일부분을 삭제하기**

```python
arr = [1, 2, 3, 4, 5]

# 인덱스 1부터 3까지 삭제 (인덱스 3은 포함되지 않음)
del arr[1:3]
print(arr)  # 출력: [1, 4, 5]
```

 3. **리스트 메서드 `pop()` 사용**
```python
arr = [1, 2, 3, 4, 5]

# 2번째 인덱스의 요소를 삭제
arr.pop(2)
print(arr)  # 출력: [1, 2, 4, 5]
```

4. **`remove()` 메서드 사용**
`remove()`는 리스트에서 **특정 값**을 삭제합니다. 값이 여러 개 있을 경우, 첫 번째로 발견된 값을 삭제합니다.

```python
arr = [1, 2, 3, 4, 3, 5]

# 값 3을 삭제 (첫 번째로 등장한 3만 삭제됨)
arr.remove(3)
print(arr)  # 출력: [1, 2, 4, 3, 5]
```

5. **리스트의 일부분을 잘라내고 원본을 수정하는 방법 추가

```python
arr = [1, 2, 3, 4, 5]

# 인덱스 1부터 3까지의 값을 8, 9로 대체
arr[1:3] = [8, 9]
print(arr)  # 출력: [1, 8, 9, 4, 5]
# 인덱스 2에 [3, 4]를 삽입

arr = [1, 2, 5, 6]
arr[2:2] = [3, 4]
print(arr)  # 출력: [1, 2, 3, 4, 5, 6]

```

### 문자열
1. 문자열 치환
```python
text = "Hello world, Hello universe"
new_text = text.replace("Hello", "Hi")
print(new_text)  # 출력: "Hi world, Hi universe"
```

2. 앞뒤 패딩 채우기

Python에서 문자열.zfill(길이) 함수를 통해 왼쪽에 0을 채울 수 있습니다.

또한 문자열.rjust(길이, 채울문자), 문자열.ljust(길이, 채울문자) 함수를 통해 왼쪽, 오른쪽을 채울 수 있습니다.

### 정렬
```python
student_tuples.sort(key=lambda x: x[2],reverse={bool})
```