
교양 과제를 위해 rstudio를 받는 것이 무거워서 
vscode에서 R언어를 사용하기 위해 설정을 하던 도중....

에러가 발생했다....

이전까지한것
https://code.visualstudio.com/docs/languages/r
이것들을해주고

경로도 야무지게 설정해줬다

```
"r.rpath.mac": "/opt/homebrew/bin/R",
"r.rterm.mac": "/Users/어쩌구/bin/radian"
```

그러나 vscode아래의 상태창에 R: no attached라는 에러가 뜨는 것이다...
하지만 놀랍게도 r을 이용한 실행은 잘 되었다..
열심히 찾다가 개발자도구를 한번 열어보라는 글을 보았다.

개발자 도구를 열어보았더니!
`[Extension Host] [updateRequest] Ignored request outside workspace`

그렇다.. 내가 연 폴더가 vscode가 워크스페이스로 등록이 안되었던것이다.

찾아보니 폴더로 열면 vscode가 자동으로 워크스페이스에 등록을 한다고한다.
그래서 다시 열었다가 닫았다를 반복하고 워크스페이스로도 등록을 해보았지만?

응 안돼~~~

안됐다...

그러다 문득 폴더명이 한글인 것이 눈에 보였다. 에이설마~ 하면서 폴더명을 영어로 바꿔줬다.

역시 잘된다..
개발자라면 폴더명은 반드시 영어로 하자..