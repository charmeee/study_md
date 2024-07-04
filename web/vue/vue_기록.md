
이미지를 동적으로 바인딩
```js
export const getImgSource = (imgPath) => {  
    return new URL(imgPath, import.meta.url).href  
}
```


style 부분에도 변수를 넣을 수 있음
v-bind(VARIABLE)
