[다이나믹프로그래밍](../theory/다이나믹프로그래밍.md) #모름 
### 문제
https://app.codility.com/c/run/trainingK7P6NV-APJ/
N 배열
정수구성 표시가능
자갈을 N-1로 옮겻을때 표시된 정수의 합
주사위 던짐 if 현재 + 주사위 == 배열인덱스, 이동&표시
else 암것도하지않음
보드에서  얻을수 있는 최대를반환

### 답
3가지 조건
전꺼랑 현재꺼랑둘다 표시
현재꺼만표시
전꺼만표시
#### WrongAnswer
```js
function solution(A) {
    let result = A[0] + A[A.length-1]
    if(A.length<=2){
        return result
    }
    let term = 0;
    for(let i = 2 ; i<A.length-1; i++){
        if(A[i]>A[i-1] && A[i]>A[i]+A[i-1]){
            term++;
            if(term<=6){
                A[i] = A[i];
                continue;
            }
        }
        term = 0
        A[i] = Math.max(A[i-1],A[i]+A[i-1])
    }
    return A.length<7? Math.max(result,result+A[A.length-2]):result+A[A.length-2]
}
```
#### RightAnswer
특정인덱스의 정답값은 이전 6개의 인덱스의 정답값 + 현재인덱스 값을 더하것임.(마지막은항상방문에해야하기에)