
### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/250136

### 답
i guess 재귀로하면 
```js
function solution(land) {
    let ans = 0
    let moves = [[0,1],[1,0],[0,-1],[-1,0]];
    let gas = new Array(land[0].length).fill(0);
    for(let i = 0; i<land.length; i++){
        for(let j = 0; j<land[i].length; j++){
            if(land[i][j] === 1 ){
                //방문시작!
                let cnt = 1;
                let visitX =  new Set([j]);
                land[i][j] = -1;
                let arr = [[i,j]];
                let arrInd = 0;
                while(arr.length-arrInd>0){
                    let [y,x] = arr[arrInd];
                    arrInd++;
                    for(let m of moves){
                        let dy = y+m[0];
                        let dx = x+m[1];
                        if(dy>-1 && dy <land.length && dx>-1 && dx <land[y].length){
                            if(land[dy][dx] === 1){
                                arr.push([dy,dx]);
                                land[dy][dx] = -1;
                                cnt++;
                                visitX.add(dx);
                            }
                        }
                    }
                }
                for(let v of visitX){
                    gas[v] += cnt;
                    if(ans<gas[v]) ans = gas[v];
                }
                // console.log(i,j)
                // console.log(gas)
            }
        }
    }
    return ans;
}
```