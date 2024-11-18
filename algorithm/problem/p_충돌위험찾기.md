[구현](../theory/구현.md)
### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/340211

n개의 좌표 (y,x) 포인트가 있음 각 포인트는 지정숫자를 가짐
로봇마다 운송경로가 존재함
routes는 포인트들의 리스트로 이뤄져있음. 해당포인트를 거처야함. 
routes[a] 는 a 번째 로봇의 운송 경로.
routes[a]의 값은 a번째 로봇이 순서대로 방문하는 포인트번호
로봇은 x대 , 0초에 출발, 1초마다 상하좌우한칸씩만 갈수 있음
이동시 항상최단경로. if 최단경로 여러개, y좌표 이동을 우선함
마지막포인트에 도착한로봇은 물류센터 벗어남, 벗어나는 경로는 고려 ㄴㄴ

2대이상모인다면 충돌할 가능성이 있는 위험상황으로 간주
위험상황을 새라

### 답
```js
	function solution(points, routes) {
    let crack = 0;
    let starts = [];
    let moves = [];
    let movesIndex = [];
    let pointCheck = {}
    for(let i = 0;i<routes.length; i++){
        let move = [];
        let before = [];
        for(let j = 0;j<routes[0].length; j++){
            let point = points[routes[i][j]-1]
            if(j===0){
                let [y,x] = point;
                if(checkCrack(pointCheck,point)) crack++;
                starts.push([y,x])
            }else{
                let dy = point[0] - before[0];
                let dx = point[1] - before[1];
                move.push([dy,dx])
            }
            before = [...point]    
        }
        moves.push(move)
        movesIndex.push(0)
    }
    // console.log(starts)
    // console.log(moves)
    // console.log(crack)
    let flag = true;
    while(flag){
        //한칸씩간다..
        flag = false;
        pointCheck = {}
        for(let i = 0; i<moves.length ; i++){
            //로봇마다..
            if(moves[i].length-1 <movesIndex[i]) {
                movesIndex[i];
                continue;
            }
            flag = true;
            let [dy,dx] = moves[i][movesIndex[i]];
            if(dy===0 && dx===0){
                movesIndex[i]++;
                continue;
            }
            if(dy!==0){
                let unit = dy/Math.abs(dy);
                starts[i][0] += unit;
                moves[i][movesIndex[i]][0] -= unit;
            }else{
                let unit = dx/Math.abs(dx);
                starts[i][1] += unit;
                moves[i][movesIndex[i]][1] -= unit;
            }
            if(checkCrack(pointCheck,starts[i])) crack++;
        }
        // console.log(starts)
        // console.log(moves)
        // console.log(movesIndex)
        // console.log(crack,flag)
        // console.log('---')
    }
    return crack;
}

function checkCrack(dict, point){
    let [y,x] = point;
    let key = `${y}${x}`
    if(dict[key]){
        dict[key]++;
        if(dict[key]===2) return true
    }else{
        dict[key]=1
    }
    return false
}


```