
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
Therefore Flux패턴 두두둥


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

