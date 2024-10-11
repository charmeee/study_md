#greedy #모름 
### 문제
https://app.codility.com/programmers/lessons/16-greedy_algorithms/max_nonoverlapping_segments/
선분 N개가 한줄에 위치
A : 시작 ,B: 끝 ,끝점을 기준으로 정렬
겹치는 경우 겹치지 않는경우
A[I] ≤ A[J] ≤ B[I] 또는 A[J] ≤ A[I] ≤ B[J]
최대로 겹치지않는 세트를 구한다.

### 답
#### Wrong Answer
각 선들마다 겹치는 선을구한다음에
겹치는선이 적은순으로 정렬해서 선택한다.
퍼포 엄청구리고 답도틀림. 내생각에는 sort시에 length뿐만아니라 index순의 조건을 추가해야한다고생각한다
```js
function solution(A, B) {
    let line = []
    let end = []
    for(let i =0;i<A.length;i++){
        line.push([i])
        end.push(B[i])
        let toggle = false
        for(let j =0;j<i;j++){
            if(!toggle && end[j]>=A[i]) toggle= true;
            if(toggle){ 
                line[j].push(i);
                line[i].push(j);
            }
        }
    }
    line.sort((a,b)=>a.length-b.length)
    let used = new Set([...line[0]]);
    let ans = 1;
    for(let i =1;i<A.length;i++){
        if(!used.has(line[i][0])){
            ans++;
            used = new Set([...used,...line[i]])
        }
    }
    return ans
}
```
#### Right Answer
걍끝점이랑 시작점이랑 겹치지않는수를 count하면된다.
```python
def solution(A, B):
    N = len(A)
    if N == 0: return 0
    if N == 1: return 1
    LINE = []
    for i in range(N):
        LINE.append([A[i], B[i]])
    LINE.sort(key=lambda x: (x[1], x[0]))
    end_point = LINE[0][1]
    cnt = 1
    for i in range(1, N):
        if end_point < LINE[i][0]:
            end_point = LINE[i][1]
            cnt += 1
    return cnt
```

```js
function solution(A, B) {
    const N = A.length;
    let res = 1;

    if (N <= 1) {
        return N;
    }

    let start = 0;
    for (let i = 1; i < N; i++) {
        if (B[start] < A[i]) {
            res++;
            start = i;
        }
    }

    return res;
}
```