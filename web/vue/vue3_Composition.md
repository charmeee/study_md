
마운트도 조금다름.
`createApp(App).mount('#app') 
ㅖㅏ 걍문법만다름

## Options와 차이점과 쓰임.
script에선 여러번 인스턴트화되더라도 한번만 실행
script setup은 인스턴스가 생성될때 마다 실행
따라서 script setup는 각 인스턴스마다 상태가 독립적으로 관리된다

그러나
SSR에서는 요청마다 새로운 vue인스턴스가 생성되기에 상태가 계속 새로 리셋됨.. 데이터 일관성도 깨질 수 있음.

## 개념과 등장이유
option는 데이터의속성 실행시점등과같이 나눴다면
composition은 관심사별로 분리를 가능캐한다.
좀더 함수형스러운듯?

script setup
혹은 export에 setup어쩌구 에만 있을 수 있음
### options
```vue
<script>
export default {
  // data()에서 반환된 속성들은 반응적인 상태가 되어 `this`에 노출됩니다.
  data() {
    return {
      count: 0
    }
  },

  methods: {
    increment() {
      this.count++
    }
  },

  mounted() {
    console.log(`숫자 세기의 초기값은 ${ this.count } 입니다.`)
  }
}
</script>

<template>
  <button @click="increment">숫자 세기: {{ count }}</button>
</template>

```
### composition
`<script setup>` 이용
```vue
<script setup>
import { ref, onMounted } from 'vue'

//toplevel 에서 비동기 사용가능 > 자동으로 async로컴파일

// 반응적인 상태의 속성
const count = ref(0)

// 속성 값을 변경하고 업데이트 할 수 있는 함수.
function increment() {
  count.value++
}

// 생명 주기 훅
onMounted(() => {
  console.log(`숫자 세기의 초기값은 ${ count.value } 입니다.`)
})
</script>

<template>
  <button @click="increment">숫자 세기: {{ count }}</button>
</template>

```

이용하지 않을시

```vue
<script>
import { ref, onMounted } from 'vue'

export default{
	setup(){
		const count = ref(0)
		// 이어서 코드 작성
		return {
			counter,
			increment
		}
	}
}
</script>
```

#### 함께사용도 가능함.
상속옵션을 끄던가 커스텀할때 script를 함께선언
```
<script>
// 일반 스크립트, 모듈 범위에서 한 번만 실행
runSideEffectOnce()

// 옵션 선언
export default {
  inheritAttrs: false,
  customOptions: {}
}
</script>

<script setup>
// 각 인스턴스 생성시 setup() 범위에서 실행
</script>
```

#### script setup의 장점 및 차이
(vue 공식 문서에 따르면...)
- 더 적은 상용구로 더 간결한 코드
- 순수 TypeScript를 사용하여 props 및 내보낼(emit) 이벤트를 선언하는 기능
- 더 나은 런타임 성능(템플릿은 중간 프락시 없이 동일한 범위의 렌더 함수로 컴파일됨)
- 더 나은 IDE 타입 추론 성능(언어 서버가 코드에서 타입을 추출하는 작업 감소)
가 있다고 한다..

> 내가생각한 단점..
> 무조건 변수나 함수가 최상위 바인딩이 되는데  이에 따른 단점이 있을꺼 같음..

script <-> script setup
script : 모듈범위에서 한번만 실행
script setup : 각 인스턴스 생성시 setup범위 내에서 실

## 통신(props emit)
```vue
<script setup>
const props = defineProps({
  foo: String
})

const emit = defineEmits(['change', 'delete'])
// ... setup 코드
</script>
```
## API 상세
https://vuejs.org/api/
총괄 API 정리도어있음
주요한 것을정리.
### 반응형(Reactivity)
data > ref(원시) , reactive(객체)
readonly option을 통해 특정 부분에서 객체 변경 방지 가능
onMounted(), onUnmounted()
![400](Pasted%20image%2020240628175728.png)
### DI
provide() inject()
provide(key,value) inject(key) : return value
광범위한 상태관리 drilling 피함
```vue
<!-- 제공자 컴포넌트 내부 -->
<script setup>
import { provide, ref } from 'vue'

const location = ref('북극')

function updateLocation() {
  location.value = '남극'
}

provide('location', {
  location,
  updateLocation
})
</script>
<!-- 제공자 컴포넌트 내부 -->
<script setup>
import { provide, ref } from 'vue'

const location = ref('북극')

function updateLocation() {
  location.value = '남극'
}

provide('location', {
  location,
  updateLocation
})
</script>
```

provide값넣을때 readonly로 감싸면 일기만 가능^&^

대규모일때는 key를 symbol로 사용하기도