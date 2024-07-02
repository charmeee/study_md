
>vuex pinia 
>pinia는 현재(vue3버전)에서 vue의 공식 상태관리 툴

- vuex가 업그레이드 된형태로 vue개발 인원중한명이 만듬
- pinia는 이전 버전인 vue2버전에서도 잘 작동함
- vuex는 actions, mutations, state 로 구성된 flux패턴
- pinia는 여기서 mutation이 빠졌음.
- pinia는 서버사이드 렌더링 지원

## vuex
리액트의 리덕스라고할수이따(리덕스도 FLUX패턴)
### FLUX
MVC패턴에서 모델과 뷰가 서로 양방향으로 영향을 받다보니
예측하기가 어려워짐 
![400](Pasted%20image%2020240702095610.png)
Therefore Flux패턴 두두둥장
단방향

- state : 여러 컴포넌트에 공유되는 데이터
	- 접근 방법 : `this.$store.state.message`
- getter : 연산된 state값을 접근하는 속성
	- 접근 방법 :  `this.$store.getters.[method]`
- mutation : state값을 변경하는 이벤트 로직
	- 접근 방법 : `this.$store.commit("function_name",인자)`
	- 사용이유
		- 사실 걍 변경을 위해선 state값에 접근해도 됨.
		- 명시적으로 상태변화수행
		- 어느 컴포넌트에서 해당 state가 변경되었는지 확인가능
		- devtool에서 관찰가능
		- 이후에사실 없어짐ㅎ,ㅎ,ㅎ,ㅎㅎ\
- action : 비동기처리로직을 선언하는 메서드
	- 접근 방법 : `this.$store.dispatch(함수 명)`
	- 사용이유
		- 언제 호출햇는지확인하기위해
		- 동기 > mutation, 비동기 > action
#### helper
앞에 map붙이면 됨
- 스프레드 연산자를 앞에 붙여야함 Why?
```
computed(){
	...mapState('num;)
	//num(){ return this.$store.state.num;}
}


```


## pinia
https://pinia.vuejs.org
option api, composition api 둘다 사용 가능함. 
- 정의 : defineStore
- 사용 : useStore

```js
// optional api
export const useCounterStore = defineStore('counter', {
  state: () => ({ count: 0, name: 'Eduardo' }),
  getters: {
    doubleCount: (state) => state.count * 2,
  },
  actions: {
    increment() {
      this.count++
    },
  },
})

// composition api
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  const name = ref('Eduardo')
  const doubleCount = computed(() => count.value * 2)
  function increment() {
    count.value++
  }
// ref > state , computed > getter, function() > action
  return { count, name, doubleCount, increment }
})
```

