[구현](../theory/구현.md)
### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/340213
10초 전이동 : if 10초 미만 , 0으로이동
10초 후이동 : if end-current <10sec , end로 이동
오프닝건너뛰기 : if current == opening구간 , opening끝으로 이동
오프닝 사이이면 자동으로 끝으로 이동해야함

### 답
단순구현문제라 쉬웠다.
```js
function solution(video_len, pos, op_start, op_end, commands) {
    video_len = convertToTime(video_len);
    pos = convertToTime(pos);
    op_start = convertToTime(op_start);
    op_end = convertToTime(op_end);
    for(let c of commands){
        pos = checkOpening(op_start,op_end,pos)
        if(c === "prev"){
            pos[1] -= 10
            if(pos[1]<0){
                pos[1] += 60
                pos[0] -= 1
                
            }
            if(pos[0]<0){
                pos = [0,0]
            }
        }else if(c === "next"){
            pos[1] += 10
            if(pos[1]>59){
                pos[1] -= 60
                pos[0] += 1
            }
            if(pos[0]>video_len[0]||(pos[0]===video_len[0]&&pos[1]>video_len[1])){
                pos = [...video_len]
            }  
        }
        // console.log(pos)
    }
    pos = checkOpening(op_start,op_end,pos)
    // console.log(pos)
    let answer = pos[0].toString().padStart(2,'0') + ':' + pos[1].toString().padStart(2,'0')
    
    return answer;
}

function convertToTime(value){
    return [parseInt(value[0]+value[1]),parseInt(value[3]+value[4])]
}

function checkOpening(start,end,current){
    if(start[0]>current[0] || (start[0]===current[0] && start[1]>current[1])){
        // 시작보다 앞이면 리턴
        return current;
    }
    if(end[0]<current[0] || (end[0]===current[0] && end[1]<current[1])){
        // 끝보다 뒤면 리턴
        return current;
    }
    return [...end]
}

```