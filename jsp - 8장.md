## 패턴
- 추상팩토리 패턴
	- 상위 객체에서 객체를 추상화하고 하위 클래스에서 구체적인 구현을 담당하는 것
- MVC
	- 모델 뷰 컨트롤러
		- 모델 : 데이터 처리 영역
			- DAO: Data Access Object 데이터베이스 연동 클래스
			- DO : Data Object 엔티티 클래스, 데이터 구조를 표현
		- 뷰
			- 화면을 구성하는 영역
			- jsp html 등
			- 기본적으로 모델,컨트롤러와 종속성이 없도록 구현.
		- 컨트롤러
			- 사용자 요청의 중심에 위치
			- 사용자 요청이 컨트롤러 -> 뷰로 이동해야함
			- 모델 -> 컨트롤러 -> 뷰
			- 뷰에 전달할때 DO 형태의 객체를 요청하고 포워딩함.
			- jsp : 간단한 기능을 구현할때 유리
			- 서블릿 : 규모확장과 스프링프레임워크로의 확장에유리
			- 구성 방법
				- 사용자 요청마다 컨트롤러 제작
				- 모듈단위로하나의 컨트롤러안에서 여러요청 단위를 구분하여 처리
				- 프런트 컨트롤러를 따로 두어 모든 요청을 하나의 컨트롤러로 모은 다음 구현컨트롤러 호출하기
	- 목적
		- 화면과 데이터 처리를 분리하여 코드간의 종속성을 줄임.
	- jsp에서의 mvp
	  ![[Pasted image 20231218223409.png|300]]

## 서블릿에서 컨트롤러 설계
기능에 따른 컨트롤러 설계
### 클라이언트 요청처리
- 처리 방법 :   단일 컨트롤러 vs 개별 컨트롤러 
- 여러 URL 패턴를 하나의 서블릿에서 처리는 가능
- BUT URL 패턴에 따라 여러개 처리는 불가 
	- /user/create /user/delete로 get  메서드 사용
		- doGet 메서드가 호출되는데 여기서 URL 패턴을 구분불가
	- 별도의 서블릿으로 처리해야함
	- BUT 같은 단위의 업무를 하나의 컨트롤러에서 처리하는 것이 관리가 쉬울 수도있음.
#### 하나의 서블릿에서 사용자 요청을 구분해 처리하는 방법
- URL 파라미터 이용
	- /user?action=create , /user?action=login
	- 파라미터는 구분가능 -> 분기처리하여서 메서드 구현
	- 단점 : 파라미터 구조가 변경되면 관련 HTML,JSP 컨트롤러의 수정이 필요함
	  ![[Pasted image 20231219002904.png|300]]
- 프런트 컨트롤러 사용
	- 모든요청의 진입점이 되는 컨트롤러가 있고 여기서 서브 컨트롤러를 호출하는구조
		- 약간 인터셉터 느뀜인듯?
	- 복잡한 구조를 체계적으로 처리가능
	- /user/create.do , /user/action.do
		- do 앞의 요청이름으로 구분하여 별도의 메서드 혹은 서브 클래스를 통해 실행
	- 장점
		- 파라미터없이 명확한 이름으로 요청가능
		- 요청에 대한 url관리가 필요없음
	- 단점
		- 세부 시스템이 분리되어잇는경우
			- 콘텍스트를 분리하는 것은 세션관리에 부담이 갈 . 수있음
		- 단일 콘텍스트에 경로로 구분하는경우
			- 프런트 컨트롤러에서 조건문과 메서드만으로 처리하는 경우임
			- 규모 커질 시 너무 비대해짐
				- 서브 컨트롤러로 포워딩 처리 필요
##### 단일 콘텍스트로 구현
조건문
```java
@WebServlet ("*.do")
public class MemberController extends HttpServlet {
	doGet (...) {
	
		String uri = request.getRequestURI();
		String conPath = request.getContextPath();
		String command = uri, substring(conPath length());
		
		switch (command) {
			case "create.do": createMember(); break; 
			case "login.do": loginMember(); break;
		}
	}
}
```
##### 서브 컨트롤러 사용하여 구현
```java
public void init(ServletConfig sc) throws ServletException {
	Map (String, SubController> contList = new HashMap<>();
	
	contList.put(" / create.do", new MemberCreateController());//서브컨트롤러 객체
	contList.put("/login.do", new LoginController());
	//각요청경로에대해 한번만 생성됨ㅋㅎ 이후엔 재사용.
｝

public void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	String url = request.getRequestURI();
	String contextPath = request.getContextPath();
	String path = url,substring(contextPath.length());
	
	SubController subController = contList.get(path);
	subcontroller.process (request, response);
｝

public interface SubController {//서브컨트롤러 인터페이스
	void process (HttpServletRequest request, HttpServletResponse response);
｝

public class MemberController implements SubController {
	void process (HttpServletRequest request, HttpServletResponse response) {
	}
}

```
##### 스프링에서 구현
에너테이션 방식
```java
@Controller
@RequestMapping(" / member")
public class MemberController {
	@PostMapping ("create")
	public void createMember () {
	}
}
```
### 입력값 핸들링
- jsp에서는 useBean 액션 이용하여 입력값을 멤버객체로
- 서블릿에서는 그런기능 ㄴㄴ 라이브러리 사용해야함
- 주로 Apache Commons BeanUtils 사용
##### 서블릿
Apache Commons BeanUtils 사용
```java
doGet (...){
	Member m = new Member());
	BeanUtils.populate (m, request.getParameterMap());
	dao.create(m);
}
```

##### SPRING
```java
@PostMapping ("create")
public void createMember (Member m) {
	dao.create(m);
}
```
#### 뷰 이동
요청처리후 적절한 뷰로 이동해야한다
- 데이터를 포함하지 않은경우
	- `response.sendRedirect( )`  : 서플릿, JSP 둘다 이거사용
- 데이터를 포함하는 경우
	- request scope object의 속성으로 데이터를 넣음.
		- 여러 데이터 포함 가능
	- session이나 application도 사용 가능
##### 서블릿
```java
doGet (){
	request.setAttribute("member", m);  // 리퀘스트 속성에 데이터넣음
	RequestDispatcher dispatcher = request.getRequestDispatcher ("userInfo.jsp");
	dispatcher.forward (request, response);
}
```
##### JSP
```jsp
<%
request,setAttribute ("member", m); 
pageContext, forwared("userInfo.jsp");
%>
```
##### SPRING
```java
@GetMapping("info")
public String getMemberInfo(int id, Model model) {
	model,addAttribute("member", m);
	return "userInfo";
}
```



## 실습

뷰 : productList.jsp, productInfo.jsp
모델 : Product.java, ProductService.java
컨트롤러 : Product.java, ProductService.java