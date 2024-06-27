
MVVM 패턴
![300](assets/vue-20240627101400036.png)
가상돔 이동

## 주요 개념
### reactivity. 반응성
데이터 바인딩 감지 > 리액트에도 잇음~
Object.defineProperty
오..님천재임? 
즉시실행함수를 이용하여 스코프 관리
## 기본 문법
data = react의 state같은거
변화를 감지해서 화면에 렌더링함
### 인스턴스 생성
```
let vm = new Vue({
	el: "#app",
	data : {
		message : "hi"
	}
})  // 관습적으로 vm사용 %%
```

## React와 차이점, 같은점

데이터흐름 양방향 vs 단방향
장단점

https://velog.io/@injoon2019/%EB%AA%85%EB%A0%B9%ED%98%95-vs-%EC%84%A0%EC%96%B8%ED%98%95-%ED%95%A8%EC%88%98%ED%98%95