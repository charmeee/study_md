
all any

find 문자열 없어도 에러안나고 -1 뜸
index 없으면 에러남 

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

### heapq
```python
import heapq heap = [] heapq.heappush(heap, 50) 
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