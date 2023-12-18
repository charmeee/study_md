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
	- COUNT(레코드 수), SUM(칼럼값 더하기), AVG(칼럼값 평균). MAX(칼럼 최댓값), MIN(칼럼 최솟값)