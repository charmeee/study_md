
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
생각한 순환 순서 : (action)>mutation> state > view 

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
this.$store.어쩌구.변수(함수)명
을 this.변수(함수)명
으로 호출 가능케함
```js
computed(){
	...mapState('num;)
	//num(){ return this.$store.state.num;}
}

```

- 스프레드 연산자를 앞에 붙여야함 Why?
	- 안에잇는 변수함수를 바깥으로거내야하니깐
 - 유연한문법
	 ```js
	 // 메서드 명 그대로시에 배열로다가 하면됨
	 ...mapMutations([
		 'clickBtn',
		 'addNumber'
	 ])
	//하지만 새로운 메서드이름으로 호출하고 싶다.
	...mapMutations({
		popupMsg:'clickBtn'
	})
	 
	```


## pinia
https://pinia.vuejs.org

option api, composition api 둘다 사용 가능함. 

- 순환 순서 : actions> state > view
- 중앙저장소 : store
	- 정의 : defineStore
	- 사용 : useStore
- 이건 내생각에는 optional이 더좋은듯
	- 왜냐면 composition으로 사용하는 큰 이유중에하나가 주제별(도메인별로) 모아주기 위해서인데
	- 상태관리는 store을 이용하기에 이미 주제별로 모아진 후이다.
```js
// 전역에서 couter로 store에 접근 가능


// optional api
export const useCounterStore = defineStore('counter', {
  state: () => ({ count: 0, name: 'Eduardo' }),
  getters: {
    doubleCount: (state) => state.count * 2,, 
	  doubledoubleCount:()=> this.doubleCount*2
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

### 왜 피니아

피니아는 Vue의 스토어 라이브러리로 컴포넌트/페이지 간에 상태를 공유할 수 있습니다. 컴포지션 API에 익숙하다면 간단한 `export const state = reactive({})`로 전역 상태를 공유할 수 있다고 생각할 수 있습니다. 이는 SPA에는 해당되지만 SSR의 경우, **앱이 [보안 취약성](https://vuejs.kr/guide/scaling-up/ssr.html#cross-request-state-pollution)에 노출됩니다.** 그러나 작은 SPA에서도 피니아를 사용하면 많은 이점이 있습니다:

- 테스트 유틸리티
- 플러그인: 플러그인으로 Pinia 기능 확장
- JS 사용자를 위한 적절한 TypeScript 지원 또는 **자동 완성**
- 서버 사이드 렌더링 지원
- Devtools 지원
    - 액션, 뮤테이션을 추적하는 타임라인
    - 사용되는 컴포넌트에서 스토어가 나타남
    - 타임 트래블 및 더 쉬운 디버깅
- 핫 모듈 교체 (HMR)
    - 페이지를 새로고침하지 않고 스토어 수정
    - 개발 중 기존 상태 유지