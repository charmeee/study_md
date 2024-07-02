
## ref
리액트의 상태관리와 머가다른가!!
### react
```js
let [num1,setNum1]=useState(1)
let num2 = num1*2;
function increment(){
	setNum1((before)=>before+1);
}

//html부분
<h2>{num1}</h2>
<h2>{num2}</h2>
  
```
![](Pasted%20image%2020240702135541.png)
state에 참조된 변수도 update된다.

### vue

