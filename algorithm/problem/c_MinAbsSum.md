### 문제
배열 A(정수로 구성),S(-1,1로구성)
$$val(A,S) = |sum{ A[i]*S[i] for i = 0..N−1 }|$$
최소화.. 양끝에 절대값이잇음ㅋㅋㅋㅋ

### 답

dp 문제인걸몰랏으면 브루드 포스를햇을거임
```
  
let minRes = Infinity
function solution(A) {
    brud(A,0,0)
    return minRes
}


function brud(A,step,sum){
    if(step>=A.length){
        let absSum=Math.abs(sum) 
        if(minRes>=absSum){
            minRes=absSum
        }
        return minRes===0
    }
    for(let i=0;i<A.length;i++){
        if(brud(A,step+1,sum-A[i])||brud(A,step+1,sum+A[i])){
            //0이나왓으므로종료한다.
            return true
        }
    }
}
```