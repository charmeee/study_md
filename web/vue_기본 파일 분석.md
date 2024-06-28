## vue 확장자

### 기존 js 에서의 코드
```
var appHeader = {
	template : '<div>header</div>',
	methods : {
		addNum : function(){
		
		}
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
}

```