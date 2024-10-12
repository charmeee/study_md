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