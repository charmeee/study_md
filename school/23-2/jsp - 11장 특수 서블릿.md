
## 리스너
- 컨테이너에서 발생하는 이벤트를 "모니터링"하다가 발생시 실행되는 특수 서플릿
- 실행에 필요한 정보 제공 
- 특정 상황에 자동으로 동작하는 프로그램을 구현할 때 사용(톰캣 시작종료 같이..)
- 애너테이션 @WebListener 를 이용해 리스너임을 명시.

### 동작구조
생명주기 변화와 해당 스코프의 속성의 변화를 관찰함.
-> 이벤트 발생 -> 리스너실행

![[../../daily/assets/Pasted image 20231219094330.png|400]]
### 활용 상황
- 초기화 매개변수와 연동
	- 톰캣이 시작시, 초기화 매개변수를 읽어 특정 개체를 초기화한 후 서블릿이나 jsp에 제공
- 예제프로그램 등 배포시 샘플데이터 제공
	- DB가 필요한 경우 , 미리 DB와의 연결을 만들어두거나 테이블을 작성하는 등의 작업을자동으로 수행해서 추가적인 작업없이 프로그램 실행할 수 있음
- 복잡한 환경 설정 제공
	- 프로그램에 필요한 여러 정보(외부서 주입하는 형태)가 고정되어있지않고 환경에 따라 변경되야하는 경우 이를 파일로부터 읽어와 JSP, 서블릿 등에 제공
- 특정 이벤트에 동작하는 기능 구현
	- 애플리케이션 실행시 함께 동작해야하는 외부프로그램이나 서비스 동작유무를 확인하고 자동 실행 가능

### 종류

- ServletContext
	- javax.servlet.ServletContextListener : 생명주기변화
	-  javax.servlet.ServletContextAttributeListener : 속성 변화
- Session
	- javax.servlet.http.HttpSessionListener : 생명주기 변화
	- javax.servlet.http.HttpSessionAttributeListener : 속성 
![[../../daily/assets/Pasted image 20231219095311.png|400]]

## 필터

- "사용자 요청"에 따라 서블릿이나 Jsp가 "실행전"에 response,request 객체의 조작이나 추가적인 처리가능
- 보통 특정 요청에만 동작, 정해진 순서에 따라 동작
- @WebFilter("url 매핑정보")
- 여러개 필터를 순서대로 적용하기
	- 'web.xml'에 필터 등록해야함
	  이경우에는 @WebFilter(filterName="filterOne")
	  ![[../../daily/assets/Pasted image 20231219101229.png|400]]

### 동작 구조
![[../../daily/assets/Pasted image 20231219100911.png|400]]
init : 초기화 작업
doFilter : 해당 필터가 적용되었을 때의 
	ServletRequest나 ServletResponse을 가로채 필요한 작업을 수행
destory : 필터가 종료될 때의 작업
### 활용상황
- 인증
- 로깅
- 국제화
- 한글 인코딩 처리