DDL, DML
JDBC
실습 9.2
## DB
여러사람이 공유할 목적으로 체계화하여 통합 관리하는 데이터 집합
DBMS : 데이터를 효과적으로 관리하고 운영하는 기능을 제공 (캐싱인덱싱 백업 권한관리등)
- 관계형 데이터페이스
	- 장점
		- 다양한 용도로 사용 가능 
		- 높은성능
		- 일관성 보장
		- 정규화 ,구조화 되어잇음.
	- 단점
		- 데이터 구조변경 어려움
		- 빠른 속도 요구하는 단순처리 대응어려움
- NoSQL
	- 테이블 형태의 구조가 아님
	- sql과 다를 수 있지만 별도의 쿼리언어나 구조는 존재
	- 장점
		- 대용량처리 유리
		- 분산처리유리
		- 빠름
		- 유연함
	- 단점
		- 복잡한 데이터 관계표현시 중복데이터 발생가능
## SQL
관계형데이터베이스 표준언어
### DDL
데이터 정의어
테이블을 생성 삭제 구조변경
- 생성
	- CREATE
	- CREATE TABLE 이름 ( 컬럼이름 자료형(크기) 제약조건|속성) 
- 수정
	- Alter
	- ALTER TABLE 이름  [ ADD | ALTER | DROP] 칼럼명 자료형 제약조건
		- alter : 자료형, 제약조건을 바꿀 수있음
- 삭제
	- Drop
	- DROP TABLE 이름 [RESTRICT | CASCADE]
- 테이블정보조회
	- SHOW
### DML
데이터 조작어
- SELECT
	  ![[Pasted image 20231219023443.png]]
- INSERT
	- INSERT INTO 테_이(칼럼이름) VALUES(칼럼데이터)
	- 컬럼에 데이터 추가
	- auto increment 거나 not null 은 안체워도 ㄱㅊ
- UPDATE
- DELETE
- JOIN
### 관련함수
- 문자관련
	- ASCII(아스키코드값), LENGTH(길이), CONCAT(문자열 결합), TRIM(양쪽 공백 제거), LOWER(소문자 변환), UPPER(대문자 변환), SUBSTRING(부분 선택)
- 날짜 기간함수
	- NOW(현재 날짜 시간), CURRENT_TIMESTAMP(현재 날짜 시간), DAYNAME(요일), PARSEDATETIME(문자열 포맷을 날짜 시간 정보로 변환)
- 집계함수 
	- COUNT(레코드 수), SUM(칼럼값 더하기), AVG(칼럼값 평균). 
	- MAX(칼럼 최댓값), MIN(칼럼 최솟값)

## JDBC
자바 애플리케이션에서 다양한 데이터베이스와  표준화된 방법으로 연결하여 개발을 위해 설계된 인터페이스
JDBC API이용해 SQL문으로 데이터 조작

### 구조
API : 개발자가 사용해서 코드를 작성하는거
드라이버 : 회사제공
![[Pasted image 20231219024244.png|300]]

### 단계
- JDBC 드라이버 로드
	- System.setProperty()
		- jdbc.drivers라는 시스템환경변수에 등록된 내용으로 하는법
	- Class.forName
		- 드라이버 이름으로 드라이버를 로드
- 데이터베이스 연결
	- java.sql.Connection
		- DriverManager.getConnection( url,"아이디","비번") : 레퍼런스 가져옴
- Statement 생성
	- java.sql.Statement
	- java.sql.preparedStatement
		- 이친구가 더조음
		- Statement 상속받기 때문에 Statement메서드 모두사용가능
		- SQL문을 미리 만들어두고 변수를 따로 입력
		![[Pasted image 20231219025219.png]]
		
- SQL문 전송
	- java.sql.Statement
		- executeQuery()
			- SELECT  수행시 사용
			- 반환값은 ResultSet클래스, 결과 데이터 접근 방법을 제공
		- executeUpdate()
			- UPDATE,DELETE
			- 반환값은 INT, 처리된 데이터 수를 반환
- 결과 받기
	- java.sql.ResultSet
		- 순차적으로 접근할 수 있는 커서를 다룰 수 있게 함.
- 연결 해제
	- java.sql.Connection
		- close()
		- 커넥션 뿐만 아니라 Statement나 ResultSet함께 종료해주는 것이 좋음.
### 실습
##### 뷰 : studentinfo.jsp
```jsp
<form method="post" action=" / jwbook / studentControl?action=insert">
	<label> 이름</ label>
	<input type="text" name="username" ><br>
	<label>대학</label>
	<input type="text" name="univ" ><br>
	<label> 생일</label>
	<input type="text" name="birth"><br>
	<label> 이메일</label>
	< input type="text" name="email" > <br> 
	<button type="submit" > 등록< /button>
</ form>
```
##### 모델 : Student.java StudentDAO.java
```java
/*Student.java  - DO클래스*/
public class Student {
	private int id;
	private String username;
	private String univ; 
	private Date birth; 
	private String email;
//생성자
//getter, setter
}

/*StudentDAO.java - DAO 클래스*/
public class StudentDAO {
	Connection conn = null;
	PreparedStatement pstmt;
	
	final String JDBC_DRIVER = "org,h2.Driver";
	final String JDBC_URL = "jdbc:h2:tcp://localhost/~/jwbookdb";

	public void open(){
		try{
				Class.forName(JDBC_DRIVER);
				conn = DriverManager.getConnection(JDBC_URL,"id","pw");
		}catch(Exception e){ e.printStactTrace(); }
	}
	
	public void close() {
		try{
			pstmt.close();
			conn.close();
		} catch (SQLException e) {  e.printStackTrace();  }
	｝
	
	public void insert(Student s) {
		open ();
		String sql ="INSERT INTO student(username, univ, birth, email) values(?,?,?,?)";
		
		try {
			pstmt = conn.prepareStatement(sq1);
			pstmt.setString(1, s.getUsername());
			pstmt.setString(2, s.getUniv());
			pstmt.setDate(3, s.getBirth());
			pstmt.setString(4, s.getEmail());
			
			pstmt.executeUpdate();
		} catch( Exception e ) { e.printStackTrace(); 
		} finally { close(); }
	}

	public List‹Student> getA11() {
		open();
		List‹Student> students = new ArrayList();
		
		try {
			pstmt = conn.prepareStatement("select * from student");
			ResultSet rs = pstmt.executeQuery();
			while(rs.next()) {
				Student s = new Student);
				s.setId(rs.getInt("id"));
				s.setUsername(rs.getString("username"));
				s.setUniv(rs.getString("univ"));
				s.setBirth(rs.getDate("birth"));
				s.setEmail(rs.getString("email"));
				
				students.add(s);
			}
		} catch (Exception e) { e.printStackTrace(); 
		} finally { close(); } 
		
		return students;
	｝
}
```
##### 컨트롤러 : StudentController.java
```java
package ch09;
import java.io.I0Exception;
import org.apache.commons.beanutils.BeanUtils;

@WebServlet ("/studentControl")
public class StudentController extends HttpServlet {
	private static final long serialVersionUID = 1L;
	
	StudentDAO dao;
	public void init(ServletConfig config) throws ServletException {
		super.init(config);
		dao = new StudentDAO();
	｝
	
	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, I0Exception {
		request.setCharacterEncoding("utf-8");
		String action = request.getParameter("action");
		String view = '';
		if(action == null) {
		getServletContext().getRequestDispatcher("/studentControl?action=list").forward (request, response);
		} else {
		switch(action) {
		case "list": view = list(request, response); break;
		case "insert": view = insert(request, response); break;
		}
		getServletContext().getRequestDispatcher("/ch09/"+view)
			.forward(request, response);
		}
	}
	
	public String list(HttpServletRequest request, HttpServletResponse response){
		request setAttribute("students", dao.getAll()); 
		return "studentInfo.jsp";
	}
	
	public String insert(HttpServletRequest request, HttpServletResponse response) {
		Student s = new Student();
		try {
			//맵을 bin객체로
			BeanUtils.populate(s, request.getParameterMap());
		} catch (Exception e) {e.printStackTrace(); }
		dao.insert(s);
		return list (request, response);
	}
}
```
