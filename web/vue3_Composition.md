
## 개념과 등장이유
option는 데이터의속성 실행시점등과같이 나눴다면
composition은 관심사별로 분리를 가능캐한다.
좀더 함수형스러운듯?
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
```vue
<script setup>
import { ref, onMounted } from 'vue'

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

`<script setup>`이부분은 아래와 같이 선언해도됨

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

## API 상세
https://vuejs.org/api/
총괄 API 정리도어있음
주요한 것을정리.
### 반응형(Reactivity)
data > ref(원시) , reactive(객체)
readonly option을 통해 특정 부분에서 객체 변경 방지 가능
### Lifecycle
### DI




+