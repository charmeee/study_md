
## 인터넷
웹 ⊂ 인터넷
![[Pasted image 20231018133545.png|400]]
- internet : 내부 네트워크 <--> Internet : 전세계가 하나로 연결된 네트워크
- 대표인터넷기반 서비스![[Pasted image 20231018140914.png|500]]
- DNS: 도메인주소 <->IP 변환.
- URI = URL에서 프로토콜 주소 포트번호제외한 경우
##  프로토콜

### TCP/IP
- 하드웨어, 운영체제 접속 매체와 관계없이 동작 가능한 개방형구조 -> 가장 널리쓰임
- OSI 7계층(네트워크 표준모델)을 단순화한 것![[Pasted image 20231018134217.png|400]]
- TCP: 데이터 흐름 관리, 정확성확인 등
- IP :  데이터를 목적지 까지 전송

## 웹구조
![[Pasted image 20231018141251.png]]
### 백엔드 중심 개발
![[Pasted image 20231018141320.png|500]]
- 주로 모놀리식 아키택쳐 방식<->REST API, 클라우드 인프라 보편화 -> MSA 방식확장
- 장점
	- SEO 좋음
	- 안정적.
	- 다양한 서버환경에 대응 가능
- 단점
	- 네트워크 부담이 큼
	- 갱신시 모든 데이터 재전송
### 프런트 중심 개발
![[스크린샷 2023-10-25 오후 6.54.22.png|500]]
- 첨에 html,js,css만 받아오고 서버로 부터 화면에 필요한 데이터만 받아와 화면을 조합해서 보여줌
- 장점
	- spa, pwa구현에 적용가능함
	- 실시간 데이터 갱신 자유로움
	- 전체화면 받아올 필요 ㄴㄴ
- 단점
	- SEO가 구림
	- 서버와 백엔드는 당연히 필요함 << 당연한거아님?
### REST API
![[스크린샷 2023-10-25 오후 7.53.05.png|500]]
- https://kimvampa.tistory.com/75
- 서버의 응답을 다양한 형태로 안전하게 전달하는 개념 ,자원의 표현에 의한 상태전달
- 데이터를 주고 받기 위한 api형태로 발전시킨 계기가 됨.
- 스프링에서는 RestController를 사용하여서 구현가능
- 자바진영에서는 JAX-RS (스프링도 이거가능)

### 컨테이너 in s/w
모듈화된 프로그램, 서로 원할하게 데이터 교환


## 서블릿
![[Pasted image 20231025193854.png|600]]
![[스크린샷 2023-10-25 오후 7.42.20.png|500]]
![[Pasted image 20231025202416.png|500]]
### 서블릿
- 톰켓(서블릿 컨테이너 역할을 함)에 의해 관리됨.
- 자바로 구연된 application server
- 스레드로 동작
- 자바로 구연하지만 서블릿 컨테이너에 해당클래스가 서블릿임을 알려줘야함
	- 2.0 web.xml이용
	- 3.0 애너테이션 이용
- 장점 
	- 자바기반으로 자바 api모두 사용가능
	- 운영체제 하드웨어 영향 ㄴㄴ => 다양한서버환경에서 실행가능
	- 다양한 오픈소스와 개발도구
- 단점
	- html과 데이터를 조합하는 방식에는 어려움이 있음
	- 단일 요청과 응답을 처리하는 구조로 다양한 경로의 url접근을 하나의 클래스에서 처리어려움
- 구현 : 둘중 하나 상속해서 구현
	- GenericServle
	- HttpServlet : 이게 html프로토콜에 최적화 되어있음
	  ![[Pasted image 20231025203200.png|500]]
		- HttpServletRequest : 클라와 연결해 처리해야할 작업 다 이 클래스 통해서.(클라 -> 서버)
		- HttpServletResponse : 클라와 연결 서버 -> 클라
- 생명주기
  ![[Pasted image 20231025203433.png|500]]
	- init : 초기화, 해당서블릿 각각의 스레드에 공통으로 작업이 있다면 init을 오버라이딩함
	- service : 이후 요청들, 스래드를 통해 동시 실행, doGet, doPost로 분기처리
		- 파라미터로 HttpServletRequest,HttpServletResponse 클래스타임인 파라미터 제공
	- destroy : 종료 , 해당서블릿에서 정리해야할 작업잇을시 이를 오버라이딩해서구현

## 스프링프레임워크
- 경량 컨테이너
	- 객체의 생명주기를 관리하며 스프링 컨테이너로부터 필요한 객체를 얻어올 수 있음
- 제어의 역행(IoC) 지원
	- 제어권이 프레임워크에 있어 필요에 따라 스프링에서 사용자 코드를 호출함
- 의존성 주입(DI) 지원
	- 각 계층이나 서비스 간의 의존성이 존재 시 프레임워크가 연결해줌
- 관점 지향 프레임워(AOP) 지원
	- 트랜젝션이나 로깅 보안과 같이 여러 모뮬에서 공통으로 사용하는 기능의 경우 해당 기능을 분리하여 관리할 수 있음
### 스프링 부트
- 스프링 간편화
- 서블릿 스택 리액티브 스택으로 구분됨
#### 서블릿 스택
- 기존 서블릿 api에 기반한 블로킹 구조를 사용함 
- 하나의 요청 하나의 스레드
#### 리액티브 스택
- 논블로킹 구조
- 서블릿 3.1이상 컨테이너 사용
- spring webflux라고하는 새로운프레임워크를 사용해 개발
- msa나 리액티브 개발 고성능 웹애플린케이션에 유리

## JSP
- 이 서플릿의 html과 데이터 결합을 쉽게 처리하기 위해 만들어짐
- html에 자바 코드를 사용할 수 있는 구조
- jsp는 html ㄴㄴ , 서블릿 형태로 변환됨.
- 서블릿으로 변견된 jsp코드는 모두 _jspService 메서드에 위치
- 커스텀 태그를 기반으로한 JSTL/EL이 도입. MVC패턴.
### 기본 문법
#### 주석
- HTML :` <!—주석—>`
- JSP : `<%—주석 ==%>`
- 차이점 : 클라에 전달 여부 ( html 클라에 전달 ㅇ, JSP 클라에 전달 ㄴㄴ)
	  
#### 지시어
`<%@ 지시어 %>`
- JSP 파일의 속성을 기술하는 문법 -> JSP컨테이너에게 어케처리하는지에 대해 담고 있음.
- page 지시어
  ![[스크린샷 2023-10-25 오후 8.45.53.png|500]]
	- `<%@ page 속성1="속성값1" 속성2="속성값2“ … %>`
	- 한글설정 : pageEncoding="UTF-8", contentType="text/html;chatsert=UTF-8"
		- JSP캐릭터셋 정의 우선순위
			- server.xml -> 각 JSP의 page지시어 “pageEncoding”속성 -> 각 JSP의 page지시어 “contentType”속성 
	 - import 다른 자바 클래스 참조. 
		 - 구분 : “ , “ or 다른 라인에 한줄더.
	- session : 기본값 true.
	- info : 해당 jsp에 대한 간단한 설명
	- errorPage, isErrorPage: 호출 에러시 불러오는 페이지를 지정하거나, 해당페이지가 오류처리 전용임을 알림.
	  
- include :  다른 html이나 Jsp파일을 포함하기 위한 기능을 제공
	- 기능 or 화면을 모듈화할 수 잇음.
	- for 정적인 페이지, 포함시켜서 컴파일
	  
- taglib :커스텀 태그(특정 기능을 태그형태로 모듈화하는 기술)라이브러리를 위한 지시어
#### 액션
`<jsp:액션 />`
- include : 다른 파일을 불러옴![[스크린샷 2023-10-25 오후 8.50.01.png|500]]
	- for 동적페이지, 실행시점에서 해당파일 호출
	- 파라미터 전달가능 전달된파일에서는 <%=request.getParameter(“email”)%> 로 파라미터 값을 사용 가능
	- [https://m.blog.naver.com/silro812/221544320261](https://m.blog.naver.com/silro812/221544320261)
- forward : 다른페이지로 전환할 때 사용![[스크린샷 2023-10-25 오후 8.51.33.png|500]]
	- response 내장객체의 sendRedirect랑 유사 but 파라미터 전달가능(파라미터공유함) url안바뀜
- plugin : 자바플러그인을 사용하여 자바 애플릿이나 자바빈즈 컴포넌트실행 가능케 한다.
- bean관련 ( usebean,setProperty,getProperty)
#### 선언
`<%! 어쩌구저쩌구 %>`
- 메서드나 멤버변수를 선언하기 위한것
- 권장 ㄴㄴ
#### 표현식
`<%= 어쩌구 %>`
- 간단한 변수를 이용한 데이터 출력이나 메서드 호출에 이용.
- 결국 out.println() 문자열로 변환됨
#### 스크립트릿
`<% 어쩌구 %>`
![[스크린샷 2023-10-25 오후 8.53.34.png|300]]
- 자바코드 거의 다 올 수 있음
- MVC 패턴이 메인이 되면서 JSP는 VIEW역할, JSTL은 커스텀 태그라이브러리,JSP 빈즈가 컨트롤용으로 사용되면서 권장사항에서 벗어남.

### 내장 객체
- JSP에서 기본적으로 잇는 객체들, 서플릿형태로 자동 변환코드에 포함되어있는 객체를 말함.
- 내장 객체자체의 생명주기를 이용하여 자바 객체의 생명주기를 관리할 수  있다.
- 내장 객체를 이용해서 서로 다른페이지에 처리된 값을 저장하고 공유할 수 잇다.
- 객체 참조 방법
  ![[Pasted image 20231025210952.png|500]]
  ![[Pasted image 20231026085341.png|500]]
  ![[Pasted image 20231026103110.png|500]]
  appli~ : 모든 사용자 데이터, session : 사용자 마다 분리된~ ,request: 페이지별로 분리된~
#### request
- 사용자 요청 관련된 기능을 제공하는 객체
- javax.servlet.http.HttpServletRequest클래스의 참조 변수
- html 폼에서 입력값을 가져올떄많이사용
```
<td>이름</td>
<td><%=request.getParameter("username") %></td>
```
  ![[Pasted image 20231025205730.png|500]]
#### response
- 사용자 응답과 관련된 기능 제공 객체
- javax.servlet.http.HttpServletResponse클래스의 참조 변수
- setContentType,sendRedirect 중요
  ![[Pasted image 20231025210002.png|500]]
#### out
- 출력 스트림 , 버퍼관련됨 메서드 잇음
- 콘솔이아니라 사용자에 전달
- javax.servlet.jsp.JspWriter
  ![[Pasted image 20231025210436.png|500]]
#### session
- session : 서버의 정보를 담은것, 사용자별로 따로 생성, 일정시간유지후 소멸
- 서버 쪽에 생성되는 내부의 공간
- javax.servlet.http.HttpSession 
- 로그인,페이지 트랙킹,장바구니 등에 사용
  ![[Pasted image 20231025210532.png|500]]
#### config
- 서블릿이 최초로 메모리 적재 시 초기화관련 정보를 저장한 객체
- web.xml에 설정된 초기화 파라미터를 참조하기위한 용도로 사용가능
  ![[Pasted image 20231025210756.png|500]]
#### application
- 웹 애플리케이션 전체를 관리하는객체
- 이걸통해 각 서플릿/jsp에서 정보 공유를 설정하고 참조 가능
- lifecycle: 톰캣시작과 종료


### 빈즈
- 자바에서 특정한 일을 독립적으로 수행하는 컴포넌트
- MVC 패턴 구현가능 jsp:view, 빈즈:model, servlet: controller
- 원래는 화면을 구성하는 위젯(GUI)을 만들기 위해 제
- 자바 빈즈<<알바 ㄴ, JSP 빈즈로  나뉨.
#### JSP 빈즈
- 웹 컨테이너에 위치
- 데이터 처리와 공용화된 기능(db연동 등)을 제공 -> 프로그램 중복 줄이고 모듈화할 수 있도록한다 -> 유지보수 쉬움
- 스크립트 <<<<JSP 빈즈
- MVC에서는 각각 JSP에서 빈즈 접근 ㄴㄴ, 컨트롤러에서 접근한다음에 각각 뷰(JSP)한테 전달
- 클래스 형태
![[Pasted image 20231025211756.png|600]]
##### 빈즈 선언
`<jsp:useBean id="addr" class="jspbook.ch07.AddrBean"/>`
- id = 빈즈의 인스턴스 이름, 스크립트에서 이걸로 빈즈를 이용.
- class = 빈즈 클래스의 클래스 이름, 패키지 경로 포함.  java파일.
- scope = 빈즈 클래스 범위.
	- page(default) : jsp 한페이지에서만 적용
	- request : request 객체를 받은 page 모두에 적용
	- session: 링크에 의해 이동하는 page 모두에 적용 (클릭을 통해서 이동하는 모든 page)
	- applicaton: 응용프로그램이 종료되는 시점까지 모든 page에 적용 됨
##### 속성 설정
`<jsp:setProperty name="addr" property="*"/>`
![[스크린샷 2023-10-25 오후 9.19.26.png|400]]
- name = 빈즈 선언시 id값에 해당.
- property = 만약 userid이라고 지정시 , 빈즈클래스의 setUserid메서드와 자동으로 매칭된다. ” * ” 시 모든 멘버변수에 setProperty가능.

##### 읽기
```
<jsp:getProperty name="mybean" property="userid” /> 
<%= mybean.getUserid() %> 
${mybean.userid}
```


## html CSS
### CSS
![[스크린샷 2023-10-26 오전 10.09.50.png|500]]
```
<!DOCTYPE html>
<html>
	<head></head>
	<body></body>
</html>
```

table tr(row), td

rowspan 새로체움
colspan 가로채움

시멘틱태그
![[Pasted image 20231026101525.png]]