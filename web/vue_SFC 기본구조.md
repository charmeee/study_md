Single File Component
확장자가 .vue인 파일
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
	},
	props : [],
}
```

### SFC에서의 코드
```
<template>
	<div>
		<div>header</div>
		<div>{{propsdata}}</div>
	</div>
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
	},
	props : ['propsdata']
}
</script>
<style>
</style>

```
function으로 감싼건 스코프를 제한하기 위해서.
### template
템플릭태그의 상위루트 태그는 하나로 묶여야함( 리액트랑같음.)