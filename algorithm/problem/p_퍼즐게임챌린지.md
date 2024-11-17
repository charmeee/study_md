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
