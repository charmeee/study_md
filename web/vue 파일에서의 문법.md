### 기존 js 에서의 코드
```
var appHeader = {
	template : '<div>header</div>',
	methods : {
		addNum : function(){
		
		}
	}
	data : {
		str: "hi"
	}
}
```

### vue 확장자에서의 코드
```
<template>
	<div>header</div>
</template>
<script>
export default {
	methods : {
		addNum : function(){
		
		}
	}
	data : function(){
		return {
			str: "hi"
		}
	}
}
</script>
<style>
</style>

```
function으로 감싼건 스코프를 제한하기
### template
템플릭태그의 상위루트 태그는 하나로 묶여야함( 리액트랑같음.)