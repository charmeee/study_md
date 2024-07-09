
이미지를 동적으로 바인딩
```js
export const getImgSource = (imgPath) => {  
    return new URL(imgPath, import.meta.url).href  
}
```


style 부분에도 변수를 넣을 수 있음
v-bind(VARIABLE)

기본적으로 id라던가 class등을 :속성 등을 통해 동적으로 바인딩된다. 이는 