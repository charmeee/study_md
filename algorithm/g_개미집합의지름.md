### 문제
https://level.goorm.io/exam/49060/%EA%B0%9C%EB%AF%B8-%EC%A7%91%ED%95%A9%EC%9D%98-%EC%A7%80%EB%A6%84/quiz/1


### 답
슬라이딩윈도우로해봤는데 안된다...
```js
// Run by Node.js
const readline = require('readline');


(async () => {
	let rl = readline.createInterface({ input: process.stdin });
	let flag = true;
	let input = []
	for await (const line of rl) {
		if(!line){
			 rl.close();
		}else{
			let arr = line.split(' ').map(x=>+x);
			input.push(arr);
		}		
	}
	let [N,D] = input[0]; //N마리 D 지름: 임의의 두 개미 사이의 거리중 가장 긴거리를 뜻함
	let point = input[1].sort((a,b)=>a-b);
	let end = point.length-1;
	// console.log(point,end)
	let current = point[end]-point[0];
	let mid = end/2;///if 6 > 2.5 , 012345
	let s = 0;
	let e = end;
	while(current>D){
		// console.log(i,current,mid)
		if(s>end || e<0)return end;
		let addStart = point[e] - point[s+1];
		let addEnd = point[e-1] - point[s];
		addStart<addEnd? s++ : e--;	
		current = Math.min(addStart,addEnd)
		// console.log(addStart,addEnd,'|',s,e);
	}
	console.log(end-(e-s));
	process.exit();
})();
//1 3 4 6 9 10
//0 1 2 3 4 5

```
