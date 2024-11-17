### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/340212
퍼즐난이도 : diff
현퍼즐 소요시간:time_cur
이전퍼즐 소요시간: time_prev
내숙련도 : level
if diff <= level , +=time_cur
if diff > level , diff-level 만큼틀림
	틀릴때마다 time_cur + time_prev
	만약풀면 앞에꺼 다시안풀어도되니깐 time_cur
limit 시간이 정해져있음
시간안에 해결할 수 있는 최소의 숙련도를 구하라.

### 답
이분탐색이용하면 될꺼가튼데?
문제를 잘못이해햇다 이전꺼전부를푸는게아니라 바로 이전꺼만 풀면되는것엿다.
```
function solution(diffs, times, limit) {
    let start = 0;
    let end = Math.max(...diffs);
    let mid;
    while(start<=end){
        let time_prev = 0
        mid = parseInt((start+end)/2)
        for(let i in diffs){
            if(diffs[i]<= mid){
                time_prev += times[i]
            }else{
                let wrong = diffs[i]-mid
                let before = i<1? 0: times[i-1]
                time_prev += before*wrong + times[i]*(wrong+1)
            }
        }
        console.log(start,end,mid,time_prev,limit)
        if(time_prev === limit) return mid
        if(time_prev<limit){
            end = mid -1;
        }else{
            start = mid + 1
        }
    }
    console.log(start,end)
    return start
}

```