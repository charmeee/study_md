### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/72413

서로다른 사람 A,B가 같은 곳에서 출발해서 각각 다른지점에 갈려고한다.
### 답
플로이드워셜일 각이 빡온다.
출발지는하나이나. 경유햇을경우!
역시맞앗다 ㅋㅋ
이때 유의해야할께 k가 가장 밖에잇어야한다는거시다.!
```js
function solution(n, s, a, b, fares) {
    //n 지점개수 , s 시작점, ab 각각 집들
    //fares [c, d, f] c<->d 의 비용 : f
    a -= 1; b -= 1; s-=1;
    let dist = [];
    for(let i =0;i<n;i++){
        let tmp = [];
        for(let j =0;j<n;j++){
            if(i===j){
                tmp.push(0)
            }else{
                tmp.push(Infinity);
            }
        }
        dist.push(tmp)
    }
    for(let i =0;i<fares.length;i++){
        let [c,d,f] = fares[i];
        if(dist[c-1][d-1]>f){
            dist[c-1][d-1] = f
            dist[d-1][c-1] = f
        }
    }
    for(let k =0;k<n;k++){
        for(let i =0;i<n;i++){
            for(let j =0;j<n;j++){
                dist[i][j] = Math.min(dist[j][i],dist[i][j],dist[i][k]+dist[k][j]);
                dist[j][i] = dist[i][j] 
            }
        }
    }
    // console.log(dist)
    let answer = dist[s][a]+dist[s][b];
    // console.log(answer)
    for(let k =0;k<n;k++){
        let tmp = dist[s][k]+ dist[k][a]+dist[k][b];
        answer = Math.min(tmp,answer)
    }
    return answer;
}
```