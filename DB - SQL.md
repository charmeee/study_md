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
#### 기본 테이블 생성
```sql
CREATE TABLE 테이블이름(
	{열이름 데이타타입  NOT NULL  DEFAULT 값,}
	PRIMARY KEY (열이름_리스트), 
	{UNIQUE (열이름_리스트),} 
	{FOREIGN KEY(열이름_리스트) REFERENCES 기본테이블(열이름_리스트) 
		ON DELETE 옵션 ON UPDATE 옵션,]} 
	CONSTRAINT 이름 CHECK(조건식)
);
```
- unique : 후보키
- not null : 속성 값 제약조건
- CASCADE : 자신이 참조하고 있는 테이블의 데이터가 삭제되면 자동으로 자신의 데이터도 삭제
	- 참조 무결성 준수 가능
- CONSTRAINT : 제약
- CHECK : 조건을 주어 해당 데이터 입력 불가능
##### example
```sql
CREATE TABLE ENROL (
	%% 속성들 정의 %%
	Sno INTEGER NOT NULL, 
	Cno CHAR(6) NOT NULL, 
	Grade INTEGER, 
	%% PK정의 %%
	PRIMARY KEY(Sno,Cno), 
	%% FK정의 %%
	FOREIGN KEY(Sno) REFERENCES STUDENT(sno) ON DELETE CASCADE ON UPDATE CASCADE, 
	FOREIGN KEY(Cno) REFERENCES COURSE ON DELETE CASCADE ON UPDATE CASCADE, 
	%% 제약조건 %%
	CHECK(Grade ³ 0 AND Grade £ 100));
```

## 데이터 조작어(DML)
>DB 데이터 관리
>입력 수정 삭제, 검색

## 데이터 제어어(DCL)
>DB 관리 및 통제
>DB 백업/복원
>사용자 등록, 권한 관리