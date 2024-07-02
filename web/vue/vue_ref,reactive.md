
## ref
리액트의 상태관리와 머가다른가!!
- 어떤값이든 가능하다
- 단! 값이 원시값이 아니면 reactive로 전환된다.
- getter, setter를 이용한다
	- 왜 와이! 
	- 
```JS
// 실제 구현이 아닌 유사 코드
const myRef = {
  _value: 0,
  get value() {
    track()
    return this._value
  },
  set value(newValue) {
    this._value = newValue
    trigger()
  }
}
```
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
<button onClick={increment}>up</button>
  
```
![](Pasted%20image%2020240702135541.png)
state에 참조된 변수도 update된다.

### vue
```js
//script 부분
const num1 = ref(1);
function increment() {
	num1.value++;
}
let num2 = num1.value * 2;
const num3 = ref(num1.value * 3);
const num4 = computed(() => {
	return num1.value * 4;
});
//IF YOU WANT TO USE WATCH
const num5 = ref(0);
watch(num1,(value)=>{
	num5.value = num1.value**6
})

//html부분
<h2>{{ num1 }}</h2>
<h2>{{ num2 }}</h2>
<h2>{{ num3 }}</h2>
<h2>{{ num4 }}</h2>
<button @click="increment">up</button>
```

![](Pasted%20image%2020240702135910.png)
참조된 변수가 업데이트 되지 않는다.
업데이트를 위해서는 watch 나 computed를 사용해야 한다.

## reactive
반응형 프록시
- 원시값을 넣으면 안바뀜 웨
```

```