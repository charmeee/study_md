> 관계형 데이터베이스 표준언어

- 관계대수 + 확장된 투플 관계 해석 기초
- 고급, 비절차적(= 사용자 친화적) 데이터언어
- 표준화
- 선언적 언어
	- 데이터 처리를 위한접근경로에 대한 명세가 불필요
- 레코드 집합 단위로 처리
- 터미널을 통해 대화식 질의어로 사용
- 프로그램에 삽입된 형태로도 사용 가능

### 테이블
- 기본 테이블 : DBMS 화일로 생성되고 저장
- 가상 테이블 : 어떤 기본 테이블로 유도되어 만들어지는 테이블
	- 독자적으로 존재 불가
- 임시 테이블 : 질의문 처리 과정의 중간 결과로 만들어지는 테이블
	- DDL 문으로 만들어지지 않음
### 스키마
- 하나의 응용(사용자)에 속하는 테이블과 기타 구성요소 등의 그룹
- 스키마이름, 스키마 소유 허가권자, 테이블, 뷰, 도메인, 기타내용에 대한 기술자
- DBA로부터 허가 받은 사용자만 소유 가능
### 카탈로그
- SQL 시스템 내에서의 한 스키마 집합
- Information_schema(DB의 메타 정보를 모아놓은 스키마) 포함
	- 실제로 레코드가 있는 것은 아님
	- read only
### 뷰
- 하나이상의 기본 테이블로부터 유도되어 만들어지는 가상테이블
- 외부스키마는 뷰와 기본테이블들의 정의로 구성
- 물리적  구현이 아님
	- 카탈로그에 SELECT-FROM- WHERE로 저장
- 뷰에 대한 내용변경 -> 테이블에 대한 변경

### 데이터 타입
- 숫자
	- 정수 : INT , SMALLINT
	- 실수 : FLOAT(n) , REAL, DOUBLE PRECISION
	- 정형 숫자 : DECIMAL(i,j), NUMERIC(i,j)
		- 전체자리수와 소수점자리수를 정의해줌.
- 문자 스트링
	- 고정 길이 문자 : CHAR(n)
	- 가변 길이 문자 : VARCHAR(n)
- 비트 스트링
	- BIT(n), BIT VARYING(n)
- 날짜
	- DATE : YY-MM-DD
- 시간
	- TIME : hh:mm:ss
	- TIMESTAMP : DATE , TIME 포함
	- INTERVAL : DATE, TIME, TIMESTAMP 포함

## 데이터 정의어(DDL)
> DB 구조 정의
> DB 객체(table, view, index etc) 생성, 수정, 삭제


### 생성 CREATE
#### 제약 조건들
- PRIMARY KEY : 기본키와 제약조건을 명세
	- UNIQUE,NOT NULL속성을 가지고 있음
- FOREIGN KEY
	- ON DELETE
	- ON UPDATE
		- CASCADE , SET NULL, NO ACTION, SET DEFAULT, RESTRICT의 옵션 잇음
- UNIQUE : 후보키(유일성,최소성 확보된 키)
- NOT NULL : 속성 값 제약조건 눌이 될 수 없다
- 삭제될때에 관한조건(기본이 RESTRICT)
	- RESTRICT : 참조하는 테이블에 데이터가 남아 있으면 참조되는 테이블의 데이터를 삭제하거나 수정할 수 없음
	- CASCADE : 자신이 참조하고 있는 테이블의 데이터가 삭제되면 자동으로 자신의 데이터도 삭제
		- 참조 무결성 준수 가능
- CONSTRAINT : 제약조건에 이름을 붙이는 것
- DEFAULT : 디폴트값지정
- CHECK : 조건을 주어 해당 데이터 입력 불가능
	- CHECK(조건)
##### CONSTRAINT 사용이유
-  CONSTRAINT 사용 경우
	```sql
	CREATE TABLE Employees (
	    emp_id INT,
	    name VARCHAR(50),
	    salary FLOAT,
	    CONSTRAINT check_salary CHECK (salary > 0)
	);
	```
	제약조건만 드랍하고 수정이 가능함
	```sql
	-- alter 는 테이블 컬럼을 수정할 때 쓰는 키워드
	ALTER TABLE Employees 
		DROP CONSTRAINT check_salary;
	
	ALTER TABLE Employees
		ADD CONSTRAINT check_salary CHECK (salary >= 50000);
```
- 사용하지 않는 경우
	```sql
	CREATE TABLE Employees (
	    emp_id INT,
	    name VARCHAR(50),
	    salary FLOAT CHECK (salary > 0)
	);
	```
	salary속성 자체를  없애고 다시만들어야함
	```sql
	ALTER TABLE Employees
		DROP COLUMN salary;
	
	ALTER TABLE Employees
		ADD COLUMN salary FLOAT CHECK (salary >= 50000);
```

#### 기본 테이블 생성
중괄호는하나무적건잇어야함 대괄호는 생략가능 + 여러번반복될수잇다. * 전체를 선택하는기호
```sql
CREATE TABLE 테이블이름(
	{열이름 데이타타입  NOT NULL  DEFAULT 디폴트값,}
	[PRIMARY KEY (열이름_리스트),] 
	{[UNIQUE (열이름_리스트),]} *
	{[FOREIGN KEY(열이름_리스트) REFERENCES 기본테이블(열이름_리스트) ]
		[ON DELETE 옵션 ] [ON UPDATE 옵션,]} 
	[CONSTRAINT 이름] [CHECK(조건식)]
);
```
예시
```sql
CREATE TABLE ENROL (
	-- 속성들 정의
	Sno INTEGER NOT NULL, 
	Cno CHAR(6) NOT NULL, 
	Grade INTEGER, 
	-- PK정의 
	PRIMARY KEY(Sno,Cno), 
	-- FK정의 
	FOREIGN KEY(Sno) REFERENCES STUDENT(sno) ON DELETE CASCADE ON UPDATE CASCADE, 
	FOREIGN KEY(Cno) REFERENCES COURSE ON DELETE CASCADE ON UPDATE CASCADE, 
	-- 제약조건 
	CHECK(Grade >0 AND Grade <100));
```
#### 뷰생성
```sql
CREATE VIEW 뷰_이름[(열_이름 리스트)] 
	AS SELECT문 [WITH CHECK OPTION]

CREATE VIEW CSTUDENT(Sno, Sname, Year)
	AS SELECT Sno, Sname, Year 
		FROM STUDENT
		WHERE Dept = '컴퓨터’
		WITH CHECK OPTION;
```
- WITH CHECK OPTION : 뷰를 통해 데이터를 변경시 뷰의 정의를 만족하는지 확인하는 옵션이다.
### 수정 삭제 DROP ALTER
#### 테이블,스키마 삭제
```SQL
DROP TABLE 테이블 이름 [조건]
DROP SCHEMA 스키마 이름 [조건]
```

#### 테이블 수정
```sql
ALTER TABLE 테이블이름 
	DROP 열이름 [조건]
	ADD 열이름 데이터타입 [DEFAULT 디폴트값] 
```

### 삭제 DELETE

## 데이터 조작어(DML)
>DB 데이터 관리
>입력 수정 삭제, 검색

### 검색 SELECT
```sql
--[]시 먼저 나오는게 디폴트 값
--DISTINCT : 중복제거
SELECT [ALL | DISTINCT] 속성 
	FROM 테이블_리스트 [WHERE 조건]
	[GROUP BY 열_리스트 [HAVING 조건]]
	[ORDER BY 열_리스트 [ASC | DESC]];
```

#### JOIN을 이용한 검색
> 가로로 합침
```sql
SELECT Sname, Dept, Grade 
	FROM STUDENT 
	JOIN ENROL 
	ON (STUDENT.Sno=ENROL.Sno) 
	WHERE ENROL.Cno = 'C413'; 

SELECT Sname, Dept, Grade
	FROM STUDENT 
	JOIN ENROL 
	USING(Sno) 
	WHERE ENROL.Cno = 'C413';
	
SELECT Sname, Dept, Grade 
	FROM STUDENT 
	NATURAL JOIN ENROL 
	WHERE ENROL.Cno = 'C413';
```
- ON은 조인할때의 기준을 정의할 때 사용한다
- USING은 조인할때 두테이블의 컬럼명(속성명)이 같을때 사용
- NATURAL JOIN은 두 테이블에 둘 다 존재하는 속성을 dbms에서 자동으로 찾아서 알아서 조인해줌
- https://doh-an.tistory.com/30

#### UNION을 이용한 검색
>새로로 합침
>UNION : 중복되는 투플제거 , UNION ALL : 중복되는 투플 제거 ㄴㄴ
>속성이 같아야 함

```sql
SELECT Sno FROM STUDENT WHERE Year = 1 
UNION 
SELECT Sno FROM ENROL WHERE Cno = 'C324';
```


#### 집계함수 
- COUNT, SUM, AVG, MAX, MIN
- 집계함수(속성) 형식
- as 써서 반환 이름 변경 가능
  ![[Pasted image 20231216170306.png|500]]
```sql
SELECT COUNT(*) AS 학생수 FROM STUDENT;
SELECT COUNT(DISTINCT Cno) FROM ENROL WHERE Sno = 300;
SELECT AVG(Midterm) AS 중간평균 FROM ENROL WHERE Cno = ‘C413’;
```
#### 부속 질의어 (서브쿼리)
##### 질의 결과가 하나인 경우
```sql
SELECT Sname, Dept 
FROM STUDENT 
WHERE Dept = 
	(SELECT Dept FROM STUDENT WHERE Sname = ‘정기태’);
```
바로 비교해도됨.

##### 질의 결과가 여러개
|   |   |
|-----|---|
|다중 행 연산자|설명|
|IN|서브쿼리의 결과에 해당 값이 존재하는지. NOT IN|
|ALL|서브쿼리의 결과랑 비교연산자 했을때 모든값이 만족하나 |
|ANY|서브쿼리의 결과랑 비교연산자 했을때 하나의 값이라도 만족하나.|
|EXISTS|서브쿼리의 결과를 만족하는 값이 존재하는지 여부를 확인하는 조건을 의미한다 NOT EXIST|
```sql
-- in  앞에 비교대상
SELECT Sname FROM STUDENT WHERE Sno IN 
	(SELECT Sno FROM ENROL WHERE Cno = 'C413');
SELECT Sname FROM STUDENT WHERE Sno NOT IN 
	(SELECT Sno FROM ENROL WHERE Cno = ‘C413’);

-- all 앞에 연산자와 비교대상
SELECT Sno, Cno FROM ENROL WHERE Final > ALL 
	(SELECT Final FROM ENROL WHERE Sno = 500);

--any 앞에 연산자랑 비교대상
SELECT column_name(s) FROM table_name WHERE column_name > ANY 
	(SELECT column_name FROM table_name WHERE condition);

-- exist 앞에 머없음
SELECT Sname FROM STUDENT WHERE EXISTS 
	(SELECT * FROM ENROL WHERE Sno = STUDENT.Sno AND Cno = 'C413');
```

### 갱신 UPDATE
```sql
UPDATE 테이블 SET { 열_이름 = 산술식} ’+ [WHERE 조건];
```

```sql
UPDATE STUDENT SET Year = 2 WHERE Sno = 300;
UPDATE COURSE SET Credit = Credit + 1 WHERE Dept = '컴퓨터';
```

SET 뒤나 WHERE뒤에 부속질의어를 써도 된다
단 SET에는 부속질의어가 하나의 값만 반환하도록 해야한다.
### 삽입 INSERT
```sql
INSERT INTO STUDENT(Sno, Sname, Year, Dept) 
VALUES (600, '박상철', 1, '컴퓨터'); 
--전부다 넣을땐 생략가능 단 순서대로..
INSERT INTO STUDENT VALUES (600, '박상철', 1, '컴퓨터');
```
#### 부속 질의문
value 부분에 넣을수있음.
```sql
INSERT INTO COMPUTER(Sno, Sname, Year) 
SELECT Sno, Sname, Year FROM STUDENT WHERE Dept = '컴퓨터';
```
### 삭제 DELETE
```sql
--조건안붙이면 레코드가 다 삭제됨
DELETE FROM 테이블 [WHERE 조건];
```
레코드를 삭제할때 부속질의문 쓰는 방식은 SELECT랑같음

## 데이터 제어어(DCL)
>DB 관리 및 통제
>DB 백업/복원
>사용자 등록, 권한 관리