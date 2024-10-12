### 문제
1 > N  두정점 u,v 거처야함
1 > u > v > N
1 > v > u > N


### 답
여러경로에 대한 최단거리를 알아야하기에 플루이드 워셜이 낫다고 판단햇다.

맞는데 시간초과가 뜬다. n^3이라서그런듯. 경로가 쨋든 정해저잇기만한다면 걍 다익스트라쓰는것이 나은가보다.

```python
import sys
import math
import heapq
input = sys.stdin.readline

N,E= map(int,input().strip().split())
graph = [[math.inf]*(N+1) for _ in range(N+1)]

for i in range(E):
    n1,n2,c = map(int,input().strip().split())
    graph[n1][n2] = c
    graph[n2][n1] = c
v1,v2 = map(int,input().strip().split())
for i in range(1,N+1):
    for j in range(i,N+1):
        for k in range(1,N+1):
            graph[k][k] = 0
            graph[i][j] = min(graph[i][j],graph[i][k]+graph[k][j])
            graph[j][i]=graph[i][j]

result = min(graph[1][v1] +graph[v1][v2]+graph[v2][N],graph[1][v2] +graph[v2][v1]+graph[v1][N])
print(result)
```
역시 킹갓 힙으로해야..
```python
import sys
import math
import heapq
input = sys.stdin.readline

N,E= map(int,input().strip().split())
graph = [[] for _ in range(N+1)]# 간선담을..
dist1 = [math.inf] * (N+1) # 1에서 무언다도착햇을때 최단거리
dist2 = [math.inf] * (N+1) # v1에서 무언가 도착햇을때 최단거리
dist3 = [math.inf] * (N+1) # v2에서 무언가 도착햇을때 최단거리

for i in range(E):
    n1,n2,c = map(int,input().strip().split())
    graph[n1].append((c,n2))
    graph[n2].append((c,n1))

# print(graph)
v1,v2 = map(int,input().strip().split())

def dij(start,dist):
    dist[start] = 0
    heap = []
    heapq.heappush(heap,(0,start))
    while heap:
        d,now=heapq.heappop(heap)
        if dist[now]<d:
            continue
        for c,n in graph[now]:
            # 인접노드 현재 거리에 이동한 거리더하기
            cost = d + c
            if cost < dist[n]:  
                # 연결하고 인접한..거힙에추가
                dist[n] = cost
                heapq.heappush(heap,(cost,n))
       
dij(1,dist1)
dij(v1,dist2)
dij(v2,dist3)
result= min(dist1[v1]+dist2[v2]+dist3[N],dist1[v2]+dist2[N]+dist3[v1])
if result == math.inf:
    result = -1
print(result)
```