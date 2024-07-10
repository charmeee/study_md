
이미지를 동적으로 바인딩
```js
export const getImgSource = (imgPath) => {  
    return new URL(imgPath, import.meta.url).href  
}
```


style 부분에도 변수를 넣을 수 있음
v-bind(VARIABLE)

------
기본적으로 id라던가 class등을 :속성 등을 통해 동적으로 바인딩된다. 이는 해당 속성의 최상단루트에 상속된다.  하지만 defineprops를 통해서 내려받을 props라고 정의를 하면 최상단루트에 상속되지 않고 변수로 값을 받아온다.
EX  그냥 속성값추가
```
>> App.vue
<Hi :id="mj" />

>> Hi.vue
<div>
hi
</div>

>> render Html
<div id=mj>
hi
</div>
```
Ex 속성값을 defineProps로 지정
```
>> App.vue
<Hi :id="mj" />

>> Hi.vue
const {id} = defineProps({id:String})
<div>
hi
</div>

>> render Html
<div>
hi
</div>


```
----
자식에게 props를넘겨줄때 나는 주로 destructing을 많이쓴다. 선언한번더안해서 개꿀이니깐 ㅎ
근데 vue에서는 state값에대해 destructing을 못쓴다. 이게 props를 넘겨줄때에도 고대로 적용된다.
```
const {userTrendData, activeId} = defineProps({  
  userTrendData: Object,  
  activeId: String  
})
```
이러면 activeId의 추적이 안된다.

```
const props = defineProps({  
  userTrendData: Object,  
  activeId: String  
})  
  
const {userTrendData, activeId} = toRefs(props);
```
이렇게해줘야한다.
`상당히 귀찮은걸 ㅎ`
왜그럴꽈

------
https://joyhong-91.tistory.com/48
reactive는재할당시반응형을 잃어버린다.

----
상위 state를 하위 state를 통해 다시선언할경우 하위 state를 바꿔도 상위 state가 따라서 바껴진다.
실험하기.

---
집가서 draggable찾아보기