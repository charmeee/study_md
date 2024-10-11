[그리디](../theory/그리디.md)
### 문제
0 <= L < N 번 로프가 일열로 바닥에
길이 배열 A[L]
인접한 로프 묶을 수 있음
k 보다 같거나 큰로프를 최대한많이 만들때의 개수

### 답	
작으면 차피 사용못하니깐 우측꺼에 연결한다고 가정한다.
그러면겁나쉽게풀림
```js
function solution(K, A) {
    let ans = 0
    for(let i = 0 ; i< A.length; i++){
        if(A[i]>=K){
            ans++;
        }else{
            if(i!==A.length-1){
                A[i+1] += A[i]
            }
        }
    }
    return ans
}
```
