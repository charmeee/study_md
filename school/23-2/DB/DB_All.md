1~4
고객 테이블 : { 고객 번호, 고객 이름, 나이, 이메일, 고객 등급, 할인율, 고객정보수정일자 } 주문정보 테이블 : { 주문번호, 고객번호, 날짜, 총 금액}

1.위의 고객 테이블에서 슈퍼(super)키, 후보(candidate)키, 기본(primary)키, 대체(alternate)키 및 보조 (Secondary)키를 구하시오.
	슈퍼키 : 유일성만 잇는거
	고객번호 고객이름 고객등급
	이메일 고객등급할인율
	등...
	후보키 : 유일성 최소성 만족
	고객번호 , 이메일
	기본키 : 후보키중 대표성 띄는것
	고객 번호
	대체키 = 보조키 후보키중 기본키제외
	이에일

2.고객 테이블을 생성하는 SQL문을 작성하시오
	CREATE TABLE CONSUMER (
		cno INT not null,
		cname VARCHAR(10),
		age INT,
		email VARCHAR(50) not null,
		rank CHAR(1),
		sale INT,
		edit_last Date,
		PRIMARY KEY(cno),
		Check ( 'A'=<rank  and rank<='C')
	);

3.주문정보 테이블을 생성하는 SQL문을 작성하시오.
	CREATE TABLE INFO (
		Ino Int not null,
		cno INT not null,
		day Date
		total INT,
		PRIMARY KEY(Ino),
		FOREIGN  KEY(cno) REFERENCE CONSUMER(cno) on delete cascade on update cascade,
	)

4.데이터베이스 무결성 제약조건(integrity constrains)들이 중요한 이유를 2번과 3번의 릴레이션을 예로 설명 하시오.
	이렇게 여러테이블간의 정보가 중복되거나 참조될 수 있는데
	만약 한곳에서만 수정을 하고 다른곳에 반영이 안되면 데이터에 일관성이 깨진다.
	sql에서는 cascade라는 명령어를 통해 무결성이 깨지는 것을 방지해준다.

5.sql 쿼리문
	![[../../../daily/assets/스크린샷 2023-12-20 오전 6.44.49.png]]
	like
	https://lcs1245.tistory.com/entry/SQL-LIKE-%EC%97%B0%EC%82%B0%EC%9E%90-%EB%AC%B8%EC%9E%90%EC%97%B4-%EB%B6%80%EB%B6%84%EC%9D%BC%EC%B9%98-%EA%B2%80%EC%83%89

7.관계대수식
	![[../../../daily/assets/스크린샷 2023-12-20 오전 6.51.55.png]]![[../../../daily/assets/스크린샷 2023-12-20 오전 6.52.08.png]]
8.SELECT 고객명, 주문번호, 상품명, 수량 FROM 고객, 주문 WHERE 고객.고객번호 = 주문.고객번호 and 수량 = (SELECT MAX(수량) FROM 주문);
	고객고 주문번호가 일치하는것들을 조인때리고 수량이 주문테이블에서 가장 많은 값이랑 같은걸 가져온다
	이중에 고객 주문번호 상품명 수량 속성만 빼서 태이블을 만든다

9.
	sql 비절차적언어로 what만 명시하면되서 사용자 관점에서 편하다
	dbms가어떻게 만들어야하는지 how를  구현하여 우리는 비절차언어로 데이터를 다룰 수 있다. 레코드 집합단위의 명령어 처리방식을 가진다.
	
10.관계 모델이 아닌 객체-관계 (Entity-Relationship) 모델을 가지고 개념적 설계를 하는 이유
	E-R모델은 상세 세부사항 구현없이 개체와 관계, 논리적인 구조에 초점을 ㅊ맞춰서 설계가 가능하다
	그리고 E-R다이어그램을 이용하면 시각적으로도 직관적으로 이해 가능하다.

11.어떤 연구소가 있다고 하자. 각 연구원은 여러 프로젝트에 참여할 수 있으면, 각 프로젝트는 최소 1명의 연 구원이 수행하며 다음과 같은 속성을 갖는다고 할 때, 적절한 객체 관계 도표를 그려보이시오. - 연구원 : {연구원번호, 이름, 이메일} - 프로젝트 : {프로젝트번호, 예산}

12.2번 내용을 바탕으로 테이블를 그려보이시오.

13.정규화 시켜야하는 이유를 작성하고, 알맞은 정규화 과정을 보여주기

14.과제 관련 느낌점, 해당 과제를 설계하게 된 동기나 이유 등등 과제 관련 질문