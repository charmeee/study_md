
이미지를 동적으로 바인딩
```
export const getImgSource = (imgPath) => {  
    return new URL(imgPath, import.meta.url).href  
}
```
