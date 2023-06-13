# 데이터베이스

## DBMS(DataBase Management System)란 무엇인가?

* 데이터를 효율적으로 관리하기 위한 소프트웨어 시스템입니다.
* DBMS는 데이터를 저장, 검색, 수정, 삭제할 수 있는 인터페이스를 제공합니다.
* DBMS의 주요 기능
    1. 저장
    2. 검색
    3. 수정
    4. 보안
    5. 무결성 : 데이터를 항상 일관되고 정확하게 유지 

## RDBMS(Relationship DataBase Management System)란 무엇인가?

* 관계형 데이터베이스 관리 시스템을 의미한다.
* 데이터를 행과 열을 통한 Table의 형태로 저장하고 관계를 연결하여 데이터를 관리합니다.
* 데이터베이스간 연결을 위해 연결을 받아오는 데이터베이스는 Foreign Key를 사용한다.

## SQL 명령어 종류 시험

### DDL(Data Definition Language) : 데이터 정의어 (데이터의 스키마를 제어 생성 삭제하는 언어 중요함)
    - CREATE : 데이터베이스 내 개체를 생성 할 때
    - DROP : 데이터베이스 내 개체를 삭제 할 때
    - ALTER : 데이터베이스 내 개체의 속성 및 정의를 변경 할 때
    - RENAME : 데이터베이스 내 개체의 이름을 변경 할 때
    - TRUNCATE : 테이블 내 모든 데이터를 빠르게 삭제할 때
```sql
CREATE TABLE MY_table(
    my_field INT,
    my_field2 VARCHAR(50),
    my_field3 DATE NOT NULL,
    PRIMARY KEY (my_field1, my_field2)
);
ALTER TABLE My_table ADD my_field4 NUMBER(3) NOT NULL;

DROP TABLE My_table;

TRUNCATE TABLE My_table;

ALTER TABLE WEXOO1H RENAME TO TMP_WEX001H_20171029175532;
```

### DML(Data Manipulation Language) : 데이터 조작 언어
    - INSERT : 특정 테이블에 데이터를 신규로 삽입할 떄
    - UPDATE : 특정 테이블 내 데이터의 전체, 또는 일부를 새로운 값으로 갱신 할 때
    - DELETE : 특정 테이블 내 데이터의 전체, 또는 일부를 삭제 할 때
    - SELECT : 특정 테이블 내 데이터의 전체, 또는 일부를 획득 할 때
```sql
# 특정 컬럼을 선택하여 입력시
INSERT INTO 테이블명(COLUMN_LIST) VALUES (COLUMN_LIST에 넣을 VALUE_LIST);
# 테이블내 모든 컬럼에 값을 입력
INSERT INTO 테이블명 VALUES (COLUMN에 넣을 VALUE_LIST);

UPDATE 테이블명 SET 컬럼명 = '갱신할 값' WHERE... ;

DELETE FROM 테이블명 WHERE... ;

SELECT 컬럼리스트 FROM 테이블명 WHERE... ;
```

### DCL(Data Control Language) : 데이터 제어 언어
* DCL의 다른 명령어들은 단독으로 사용되는 경우가 많습니다.
    - GRANT : 데이터베이스 사용자에게 특정 작업의 수행 권한을 부여할 떄
    - REVOKE : 데이터베이스 사용자에게 부여권 수행 권한을 박탈할 때
    - SET TRANSACTION : 트핸잭션 모드로 설정 할 때
    - BEGIN : 트랜잭션의 시작을 의미
    - COMMIT : 트랜잭션을 실행 할 때
    - ROLLBACK : 트랜잭션을 취소 할 때
    - SAVEPOINT : 콜백 지점을 설정 할 떄
    - LOCK : 테이블 자원을 점유 할 떄

## RDBMS에서 N:n의 관계 유형
* 1:1 : 고유한 값을 가진 하나의 테이블의 레코드가 다른 테이블의 레코드와 하나의 대응 관계를 가지는 것.
* 1:n : 고유한 값을 가진 하나의 테이블의 레코드가 여러 테이블 레코드와 대응 관계를 가지는 것.
* n:m : 하나의 데이터베이스가 여러 데이터베이스와 관계를 맺을 수 있고 반대도 가능한 다대다 관계의 테이블을 의미
```sql
학생 (students) 테이블:
- 학생 ID (student ID, PK)
- 학생 이름 (student name)
- 학생 성별 (student gender)
- 학생 나이 (student age)
- ... 1:n

과목 (subjects) 테이블:
- 과목 ID (subject ID, PK)
- 과목 이름 (subject name)
- 과목 교수 (subject professor)
- 과목 학점 (subject credit)
- ... 1:m

수강 (enrollment) 테이블:
- 학생 ID (student ID, FK)
- 과목 ID (subject ID, FK)
- 수강 학기 (semester)
- 수강 성적 (grade)
- ... n:m 

```

**레코드(record)는 각 테이블의 행(row), 데이터의 단일 인스턴스**

## 관계형 데이터베이스 구축 절차
1. 요구사항 분석 : 사용 목적과 필요한 데이터를 파악하여 모델링을 수행
2. 개념적 설계 : 모델링을 통해 스키마, 엔티티, 관계 등의 개념을 정의
3. 논리적 설계 : 관계 스키마, 속성, 제역 등을 정의
4. 물리적 설계 : 데이터베이스 서버의 용량, 성능을 고려하여 스토리지 구성, 인덱스 디자인을 수행
5. 구현 : 데이터베이스 생성, 테이블 생성, 인덱스 생성 등을 수행
6. 데이터 입력 : 구현된 데이터베이스에 데이터를 입력
7. 테스트 및 검증 : 데이터의 정확성, 일관성, 무결성 등을 검증
8. 운영 및 유지보수 : 백업 및 복구, 인덱스 재조정 등을 수행하여 데이터베이스의 성능을 최적화

## 모델링 절차
1. 개념적 모델링 : 업무 분석 단계에서 진행 
2. 논리적 모델링 : 업무 분석의 후반부와 시스템 설계 전반부에 걸쳐서 진행
3. 물리적 모델링 : 시스템 설계의 후반부에 진행

## 요약된 SELECT문의 형식 (시험)
SELECT select_expr 
**결과 집합에 포함할 열을 지정합니다. 하나 이상의 열을 지정하거나 와일드카드 기호(*)를 사용하여 모든 열을 선택할 수 있습니다.**
1. [FROM table_references] : 조회할 테이블을 지정합니다. 하나 이상의 테이블을 지정할 수 있으며 JOIN 절을 사용하여 테이블을 결합할 수 있습니다.
2. [WHERE where_condition] : 결과 집합에 포함되기 위해 데이터가 충족해야 하는 조건을 지정합니다. AND 및 OR와 같은 논리 연산자를 사용하여 조건을 결합할 수 있습니다.
3. [GROUP BY group_by_expression] : 결과 집합을 하나 이상의 열로 그룹화합니다. 이것은 종종 COUNT 또는 SUM과 같은 집계 함수와 함께 사용되어 각 그룹에 대한 요약 통계를 계산합니다.
4. [HAVING having_condition] : 결과 집합에 포함되기 위해 그룹화된 데이터가 충족해야 하는 조건을 지정합니다. 이는 WHERE 절과 유사하지만 개별 행이 아닌 그룹에서 작동합니다.
5. [ORDER BY order_expression] : 행이 반환되어야 하는 순서를 지정합니다. 하나 이상의 열을 기준으로 정렬할 수 있으며 각 열에 대해 오름차순 또는 내림차순을 지정할 수 있습니다.

**테이블은 새로운공간에 가져와 생성하는 것이다.**
```sql
Use mysql;
SELECT * FROM employees.employees;
```
* mysql 스키마 사용
* employees 데이터베이스의 employees 테이블 가져오기
* result set으로 SELECT한 형식의 데이터 베이스 열 행을 가져온다

**데이터를 가져오기위해 선정해야하는 우선순위**
1. 단열 단행 : 특정 값의 1개의 데이터를 목저으로 자원소모를 최소한으로 정확한 값을 가져오는게 중요하다.
2. 단열 다행
3. 다열 다행 : 지양해야 하는 방식

**워크벤치에서 스키마 지정 후 사용할 수 있는 쿼리문**
```sql
SELECT * FROM employees;
SELECT * FROM titles;
```

**특정 열의 테이블 데이터 가져오기**
```sql
SELECT first_name FROM employees;
SELECT first_name, last_name, gender From employees;
```

**LIMIT로 제한된 데이터 가져오기**
```sql
SELECT * FROM employees ORDER BY birth_date ASC LIMIT 10;
```

**INSERT INTO '테이블 명'으로 테이블에 데이터 삽입하기**
```sql
INSERT INTO userTBL VALUES * FROM ('YJS', '유재석', 1972, '서울', '010', '11111111', 178, '2008-8-8');
INSERT INTO userTBL VAlUES('YJS', '유재석', 1972, '서울', '010', '11111111', 178, '2008-8-8');
```

**테이블 생성하기** 
```sql
CREATE TABLE userTBL
{
    userID CHAR(8) NOT NULL PRIMARY KEY, -- 사용자 PK
    userName    	VARCHAR(10) NOT NULL, -- 이름
    mDate    	DATE  -- 회원 가입일
}
```

**쿼리문 연산자 사용 (IN 시험 문제)**
```sql
-- 회원 테이블에서 1970년 이후에 출생, 키 182cm 이상인 아이디 이름 조회
SELECT userID, userNAME, FROM userTBL WHERE birthYear >= 1970 AND height >= 182;

-- 회원 테이블에서 1970년 이후에 출생했거나 키 182cm 이상인 아이디 이름 조회
SELECT userID, userNAME, FROM userTBL WHERE birthYear >= 1970 OR height >= 182;

SELECT userName, addr FROM userID WHERE addr='경남' OR addr='충남' OR addr='경북';
SELECT userName, addr FROM userID WHERE addr IN ('경남', '충남', '경북'); -- in function 힘수 중요!! 1개 라도 해당하면
```

**와일드 문자 사용**
```sql
SELECT userName, height FROM userTBL WHERE userName LIKE '_경규';
        -- LIKE 김으로 시작하는 모든 것
SELECT userName, height FROM userTBL WHERE userName LIKE '김%';
        -- LIKE _ 언더바는 한개의 문자 어떤 한 문자와 경규가 있는 데이터를 가져옴
```

**서브 쿼리문 사용 시험**
```sql
SELECT userName, height FROM userTBL WHERE height > (SELECT height FROM userTBL WHERE userName = '김용만'); 
-- userTBL에 유저 이름 '김용만'의 키보다 큰 키의 데이터의 userName, height

SELECT userName, height FROM userTBL WHERE height >= (SELECT height FROM userTBL WHERE addr = '경기');
-- 에러 코드 단일 단행이 아니다


-- ANY
SELECT userName, height FROM userTBL WHERE height >= ANY (SELECT height FROM userTBL WHERE addr = '경기');

-- ALL
SELECT userName, height FROM userTBL WHERE height >= ALL (SELECT height FROM userTBL WHERE addr = '경기');

-- IN 서브 쿼리문
SELECT userName, height FROM userTBL WHERE height IN (SELECT height FROM userTBL WHERE addr = '경기'); -- (180, 176) 과 구조가 같음
```
* 서브쿼리문은 비교를 위해 상수로 가져와야 한다
* 첫 예시는 단열 단행을 가져오는 효율적인 문장

* ANY를 통해 주소가 '경기'데이터를 가진 여러 행을 1가지 구조로 바꿔준다
* ANY로 가져온 데이터들 중 값이 큰 아무거나로 가져오게 된다

* ALL은 ANY와 같이 데이터를 가져옴
* 대신 2가지 요건을 모두 충족하는 데이터를 가져옴 (180, 176 이상인 필드)

* IN 키워드는 속한 비교값과 똑같은 값을 가져오라는 조건을 가짐

**order by 키워드로 정렬하기**
```sql
SELECT userName, mDate FROM userTBL ORDER BY mDate ASC;
SELECT userName, mDate FROM userTBL ORDER BY mDate DESC;

-- 섞어 쓰기
SELECT userName, height FROM userTBL ORDER BY height DESC, userName ASC; 
```
* ASC키워드는 오름 차순으로 받아오기 1 2 3 4 ...
* DESC키워드는 내림 차순으로 받아오기
* 섞어쓰기 : height로 내림차순하고 같은 값이 나오면 username으로 오름차순 정렬하기

**DISTINCT 겹치는 데이터가 있으면 1개만 출력하도록 만들기**
```sql
-- 중복 정렬되는 주소들 확인
SELECT addr FROM userTBL ORDER BY addr;

-- DISTINCT로 1개씩만 출력되게 만들기 
SELECT DISTINCT addr FROM userTBL; 
```

```
트리거 안나옴 
데이터 CRUD
데이터베이스 생성해서 관계맺기 > 데이터 베이스 관계 3가지 중에서 맺고 사용하기
테이블 생성 & 테이블 열에 형식 지정, 제약 사항 지정 (테이블 내용)
테이블 CRUD
select 정렬 (원하는 행만 가져오기 where)
            (그룹을 지어서 sum min max 등 등 사용)
            (단일 행 단일 열 단일 열 다중 행 in any all 짤수 있고 알아야함)
```

# 5주차

### SELECT로 테이블 데이터 읽어오기
```sql
SHOW DATABASES;

SELECT * FROM employees.employees; -- employees 데이터베이스에서 employees 테이블의 모든 열을 선택

SELECT first_name, gender From employees LIMIT 10; -- employees테이블에서 10 개만 first_name, gender 선택

SELECT * FROM employees ORDER BY birth_date ASC LIMIT 10; -- employees테이블의 모든 열에서 birth_date 오름차순을 기준으로 정렬하여 10개만 선택
SELECT * FROM employees ORDER BY first_name DESC LIMIT 10; -- employees테이블의 모든 열에서 first_name 내림차순을 기준으로 정렬하여 10개만 선택

SELECT userID, userName FROM userTBL WHERE birthYear >= 1970 AND height >= 182; -- userTBL 테이블에서 birthYear>=1970 이면서 height>182 userID, userName 
SELECT userID FROM userTBL WHERE birthYear >= 1970 OR height >= 182 --userTBL 테이블에서 birthYear>=1970 이거나 height>182 userID
```

* **in function 함수!!**
```sql
SELECT userName FROM userTBL WHERE addr IN ('경남','충남','경북'); -- userTBL 테이블에서 addr이 경남, 충남, 경북 3개중에 1개인 userName 선택  
```

* **와일드 문자**
    - 김% :LIKE 김으로 시작하는 모든것
    - _경규 : _ 언더바는 한개의 어떤 한 문자와 경규가 있는 문자를 모두
```sql
SELECT userName, height FROM userTBL WHERE userName LIKE '_경규';
SELECT userName, height FROM userTBL WHERE userName LIKE '김%';
```

* **()를 사용한 서브 쿼리문 시험!!**
    - ()안에 작성하면 서브 쿼리문이라고 함
    - 코드의 서브쿼리문 값 : 177
    - 서브쿼리문 단일 단행이어야 한다
    - 서브쿼리문은 비교를 위해 상수로 가져와야 한다
```sql
SELECT userName -- userTBL 테이블에서 height가>=(userTBL 테이블에서 userName이'김용만'인 height 값 선택) userName 선택
    FROM userTBL WHERE height > (SELECT height FROM userTBL WHERE userName = '김용만');

SELECT userName, height FROM userTBL -- userTBL 테이블에서 height가>=(userTBL 테이블에서 addr='경기'인 height값 중 큰 아무값) userName 선택
    WHERE height >= ANY(SELECT height FROM userTBL WHERE addr = '경기'); -- (180 ~ 176 사이의 모든 값)
SELECT userName, height FROM userTBL -- userTBL 테이블에서 height가>=(userTBL 테이블에서 addr='경기'인 모든 height값 ) userName 선택
    WHERE height >= ALL(SELECT height FROM userTBL WHERE addr = '경기'); -- (180, 176 보다큰 사이의 모든 값)
SELECT userName, height FROM userTBL 
   WHERE height >= IN(SELECT height FROM userTBL WHERE addr = '경기'); -- (180, 176 두값과 같은 모든 값)
```
+ ALL과 ANY는 다행을 1개의 단일 단행으로 만들어 준다다
+ ALL은 여러가지 요건을 모두 충족하는 데이터를 가져옴
+ ANY를 통해 여러 조건중 큰 아무 값을 가져옴

* **DISTINCT 겹치는 요소가 있으면 1개만 출력하도록 만들기**
```sql
SELECT addr FROM userTBL ORDER BY addr; -- 중복 정렬되는 주소들 확인
SELECT DISTINCT addr FROM userTBL ORDER BY addr DESC; -- DISTINCT로 1개씩만 출력되게 만들기
```
* 열의 타입의 여러 종류를 보기 위해서


# 6주차

### LIMIT 함수
```sql
SELECT emp_no, hire_date FROM employees 
   ORDER BY hire_date ASC
   LIMIT 5;

SELECT emp_no, hire_date FROM employees 
   ORDER BY hire_date ASC
   LIMIT 2, 5;  -- LIMIT 5 OFFSET 2와 동일
```

### 테이블 복사
```sql
USE cookDB;   
CREATE TABLE buyTBL2 (SELECT * FROM buyTBL); -- buyTBL테이블을 복사하여 새 테이블 buyTBL2 생성
CREATE TABLE buyTBL3 (SELECT userID, prodName FROM buyTBL); -- buyTBL 특정 열 테이블을 복사하여 새테이블 buyTBL2 생성
```

### 집계 함수
1. COUNT(): 해당 칼럼의 값의 개수를 반환합니다.
2. SUM(): 해당 칼럼의 값의 합을 반환합니다.
3. AVG(): 해당 칼럼의 값의 평균을 반환합니다.
4. MAX(): 해당 칼럼의 값 중 최대값을 반환합니다.
5. MIN(): 해당 칼럼의 값 중 최소값을 반환합니다.
```sql
SELECT COUNT(mobile1) AS '휴대폰이 있는 사용자' FROM userTBL;

SELECT userID AS '사용자 아이디', SUM(price * amount) AS '총 구매액'
	FROM buyTBL GROUP BY userID;

SELECT userName, height
	FROM userTBL
    WHERE height = (SELECT MAX(height) FROM userTBL)
		OR height = (SELECT MIN(height) FROM userTBL);

SELECT userID AS '사용자', SUM(price*amount) AS '총구매액'  
   FROM buyTBL 
   GROUP BY userID
   HAVING SUM(price*amount) > 1000 ;
```
* where에는 집계함수 못씀 그래서 조건을 주려면 having을 사용
* pk, fk를 가진 해당 테이블 값 가저온 후 다음 테이블로 넘어가야 함

### 데이터 삽입
```sql
USE cookDB;
CREATE TABLE testTBL1 (id int, userName char(3), age int);
INSERT INTO testTBL1 VALUES (1, '뽀로로', 16);
INSERT INTO testTBL1 VALUES (2, '크롱');
INSERT INTO testTBL1(userName, age, id) VALUES ('루피', 14, 3); -- 데이터 데이블 구조 변경
```
### 데이터 삽입 N:M의 관계의 데이터 베이스 생성
```sql
CREATE TABLE testTBL2 (id int AUTO_INCREMENT KEY, -- 시험 AUTO_INCREMENT KEY N:M의 관계 테이블 을 만들떄 주로 사용
    userName char(3),
    age int);
INSERT INTO testTBL2 VALUES (NULL, '에디', 15);
INSERT INTO testTBL2 VALUES (NULL, '포비', 12);
```

### 테이블 수정
```sql
ALTER TABLE testTBL2 AUTO_INCREMENT = 100;
INSERT INTO testTBL2 VALUES (NULL, '패티', 13);
SELECT * FROM testTBL2;
```

### 테이블 시스템 변수
```sql
CREATE TABLE testTBL3
    (id INT AUTO_INCREMENT PRIMARY KEY,
    userName char(3),
    age int);

ALTER TABLE testTBL3 AUTO_INCREMENT=1000; -- AUTO_INCREMENT의 값 1000 설정
SET @@auto_increment_increment = 3; -- AUTO_INCREMENT의 증가 값 3 씩 설정
INSERT INTO testTBL3 VALUES (NULL, '우디', 20);
INSERT INTO testTBL3 VALUES (NULL, '버즈', 18);
SELECT * FROM testTBL3;
```
* @test = 10 : 사용자 변수(@ 1개) 
* @@auto_increment_increment = 3 : 시스템 변수(@@ 2개) 

### INTO를 통해 이미 만들어진 테이블에 원소 추가
```sql
CREATE TABLE testTBL4 (id int, Fname varchar(50), Lname varchar(50));
    INSERT INTO testTBL4
        SELECT emp_no, first_name, last_name
            FROM employees.employees;

CREATE TABLE testTBL6 
    (SELECT emp_no AS id, first_name AS Fname, last_name AS Lname
        FROM employees.employees);
SELECT * FROM testTBL6 LIMIT 3;
```

### UPDATE 
```sql
USE cookDB;
UPDATE testTBL4
    SET Lname = '없음'
    WHERE Fname = 'Mary';
SELECT Fname = 'Mary' FROM testTBL4;

UPDATE buytbl SET price = price * 1.5;
```

### Delete
```sql
USE cookDB;
CREATE TABLE bigTBL1 (SELECT * FROM employees.employees);
CREATE TABLE bigTBL2 (SELECT * FROM employees.employees);
CREATE TABLE bigTBL3 (SELECT * FROM employees.employees);

DELETE FROM bigTBL1;
DROP FROM bigTBL2;
TRUNCATE bigTBL3;
```
* DROP : 데이터 포함 스키마까지 젠부 제거 (속도 제일 느림)
* DELETE : 제거 로그가 뜨고 데이터만 제거 (속도 제일 빠름)
* TRUNCATE : 스키마는 남기고 데이터만 전부 제거 (DROP에 비해 빠름 로그는 안뜸)

### 쿼리 문장이 에러여도 다음 문장 실행하기
```sql
INSERT IGNORE INTO memberTBL VALUES ('KHD', '강호동', '미국');
INSERT IGNORE INTO memberTBL VALUES ('KHD', '강후덜', '한국');
```

### 순위함수 OVER
```sql
SELECT ROW_NUMBER( ) OVER(ORDER BY height DESC) AS '키큰순위'
    ,userName, addr, height FROM userTBL;
SELECT ROW_NUMBER( ) OVER(ORDER BY height DESC)
    ,userName, addr, height FROM userTBL;
SELECT ROW_NUMBER( ) OVER(ORDER BY height DESC, userName ASC) , userName, addr, height
	FROM userTBL;
```
### 윈도우 함수 PARTITION BY
```sql
SELECT addr, ROW_NUMBER( ) OVER(PARTITION BY addr) '지역별 키큰 순위'
    , userName, height FROM userTBL;
SELECT addr, ROW_NUMBER( ) OVER(PARTITION BY addr ORDER BY height DESC, userName ASC) '지역별키큰순위'
    , userName, height FROM userTBL;
```

# 기말고사 범위

## 8장 

### INNER JOIN
```sql
USE cookDB;
SELECT *
    FROM buyTBL
        INNER JOIN userTBL
            ON buyTBL.userID = userTBL.userID
    WHERE buyTBL.userID = 'KYM';

-- 테이블을 명시하는 코드
SELECT buyTBL.userID, userTBL.userName, buyTBL.prodName, userTBL.addr, CONCAT(mobile1, mobile2) AS '연락처'
    FROM buyTBL
        INNER JOIN userTBL
            ON buyTBL.userID = userTBL.userID;

-- 테이블 명시를 ID화 하여 간소화
SELECT B.userID, U.userName, B.prodName, U.addr, CONCAT(U.mobile1, U.mobile2) AS '연락처'
    FROM buyTBL AS U
        INNER JOIN userTBL B
            ON B.userID = U.userID;
-- DISTINCT를 통해 ID 유니크하게 만들어 중복 요소를 제거
SELECT DISTINCT U.userID, U.userName, U.addr
    FROM userTBL U
        INNER JOIN buyTBL B
            ON U.userID = B.userID
        ORDER BY U.userID;

-- 2단 JOIN 
USE cookDB;
CREATE TABLE stdTBL 
( stdName    VARCHAR(10) NOT NULL PRIMARY KEY,
  addr	  CHAR(4) NOT NULL
);
CREATE TABLE clubTBL 
( clubName    VARCHAR(10) NOT NULL PRIMARY KEY,
  roomNo    CHAR(4) NOT NULL
);
CREATE TABLE stdclubTBL
(  num int AUTO_INCREMENT NOT NULL PRIMARY KEY, 
   stdName    VARCHAR(10) NOT NULL,
   clubName    VARCHAR(10) NOT NULL,
FOREIGN KEY(stdName) REFERENCES stdTBL(stdName),
FOREIGN KEY(clubName) REFERENCES clubTBL(clubName)
);
INSERT INTO stdTBL VALUES ('강호동','경북'), ('김제동','경남'), ('김용만','서울'), ('이휘재','경기'),('박수홍','서울');
INSERT INTO clubTBL VALUES ('수영','101호'), ('바둑','102호'), ('축구','103호'), ('봉사','104호');
INSERT INTO stdclubTBL VALUES (NULL, '강호동','바둑'), (NULL,'강호동','축구'), (NULL,'김용만','축구'), (NULL,'이휘재','축구'), (NULL,'이휘재','봉사'), (NULL,'박수홍','봉사');

-- 다대다 관계 테이블은 3단관계로 쌓여있기에 조인을 2번해야 전체적인 테이블 구조가 나온다.
SELECT S.stdName, S.addr, C.clubName, C.roomNo
    FROM stdTBL S
        INNER JOIN stdclubTBL SC
            ON S.stdName = SC.stdName
        INNER JOIN clubTBL C
            ON SC.clubName = C.clubName
    ORDER BY S.stdName; -- ORDER BY C.clubName;
```

### OUTER JOIN
```sql
-- LEFT OUTER JOIN : 처음쓴 기준에서 데이터 테이블
SELECT U.userID, U.userName, B.prodName, U.addr, CONCAT(U.mobile1, U.mobile2) AS '연락처'
    FROM userTBL U
        LEFT OUTER JOIN buyTBL B
            ON U.userID = B.userID
    ORDER BY U.userID;
-- RIGHT OUTER JOIN : JOIN 문 기준에서 사용한 데이터 테이블
SELECT U.userID, U.userName, B.prodName, U.addr, CONCAT(U.mobile1, U.mobile2) AS '연락처'
    FROM userTBL U
        RIGHT OUTER JOIN buyTBL B
            ON U.userID = B.userID
    ORDER BY U.userID;
-- 한번도 구매하지않은 유저 목록 출력
SELECT U.userID, U.userName, B.prodName, U.addr, CONCAT(U.mobile1, U.mobile2) AS '연락처'
    FROM userTBL U
        LEFT OUTER JOIN buyTBL B
            ON U.userID = B.userID
    WHERE B.prodName IS NULL
    ORDER BY U.userID;

-- 수영을 가져오기 위한 2단 아우터
SELECT C.clubName, C.roomNo, S.stdName, S.addr
    FROM stdTBL S
        LEFT OUTER JOIN stdclubTBL SC
            ON S.stdName = S.stdName
        RIGHT OUTER JOIN clubTBL C
            ON SC.stdName = C.stdName
    ORDER BY C.clubName ;

-- 동아리에 가입하지 않은 학생과 학생이 한 명도 없는 동아리도 출력
SELECT S.stdName, S.addr, C.clubName, C.roomNo
   FROM stdTBL S 
      LEFT OUTER JOIN stdclubTBL SC
          ON S.stdName = SC.stdName
      LEFT OUTER JOIN clubTBL C
          ON SC.clubName = C.clubName
UNION   -- 데이블 두개를 다 연산하기 위한 유니온 (합집합) & 중복이 제거 된다.
        -- UNION ALL : 중복되는 값도 모두 가져온다.
SELECT S.stdName, S.addr, C.clubName, C.roomNo
   FROM  stdTBL S
      LEFT OUTER JOIN stdclubTBL SC
          ON SC.stdName = S.stdName
      RIGHT OUTER JOIN clubTBL C
          ON SC.clubName = C.clubName;

-- CROSS JOIN : 한 행에대한 비교 테이블의 보든 행을 조인함
SELECT * 
   FROM buyTBL 
     CROSS JOIN userTBL ;
```

### sql if else 문
```sql
DROP PROCEDURE IF EXISTS ifProc2; 
USE employees;
DELIMITER $$
BEGIN
    DECLARE hireDATE DATE;
    DECLARE curDATE DATE; 
    DECLARE days INT;

    SELECT hire_date INTO hireDATE
        FROM employees.employees
	    WHERE emp_no = 10001;
    SET curDATE = CURRENT_DATE(); -- 현재 날짜
	SET days =  DATEDIFF(curDATE, hireDATE); -- 날짜의 차이, 일 단위

    IF (days/365) >= 10 THEN
        SELECT CONCAT('10년차 이상 입사한지 ', days, '일이나 지났습니다.') AS '메시지';
    ELSE IF (days/365) >= 5 THEN 
        SELECT CONCAT('5년차 이상 입사한지 ', days, '일이나 지났습니다.') AS '메시지';
    ELSE 
        SELECT '입사한지 ' + days + '일밖에 안되었네요.' AS '메시지';
END IF;
END $$
DELIMITER ;

CALL ifProc2();
```
### sql case end 문
```sql
SELECT U.userID, U.userName, SUM(price*amount) AS '총구매액',
    CASE
        WHEN (SUM(price*amount)>=1500) THEN '최우수 고객'
        WHEN (SUM(price*amount)>=1000) THEN '우수 고객'
        WHEN (SUM(price*amount)>=1) THEN '일반 고객'
        ELSE '유령고객'
    END AS '고객 등급'
    FROM buyTBL B
        RIGHT OUTER JOIN userTBL U
            ON B.userID = U.userID
        GROUP BY U.userID, U.userName 
        ORDER BY sum(price*amount) DESC ;
```
### PREPARE 
#### PREPARE 미리 명령문을 만들어 놓고 계속 사용 가능 
#### PREPARE를 제거해주지 않으면 메모리를 차지해 효율이 별로임 고로 사용 제거문을 만들어야함
#### 아예 안쓰게 되면 DEALLOCATE PREPARE을 통해 할당을 빼줘야 한다
```sql
use cookDB;

PREPARE myQuery FROM 'SELECT * FROM userTBL WHERE userID = "NHS"';

EXECUTE myQuery;

DEALLOCATE PREPARE myQuery;
```

### REFERENCES : 데이터 무결성을 보장해 준다.
```sql
CREATE TABLE buyTBL 
(  num INT AUTO_INCREMENT NOT NULL PRIMARY KEY , 
   userID  CHAR(8) NOT NULL, 	
   prodName CHAR(6) NOT NULL,
   groupName CHAR(4) NULL , 
   price     INT  NOT NULL,
   amount    SMALLINT  NOT NULL 
  , FOREIGN KEY(userID) REFERENCES userTBL(userID)
);
```
### CONSTRANT : 제약조건 설정
```sql
CREATE TABLE userTBL 
( userID  CHAR(8) NOT NULL, 
  userName    VARCHAR(10) NOT NULL, 
  birthYear   INT NOT NULL,  
  CONSTRAINT PRIMARY KEY PK_userTBL_userID (userID) 
  -- 사용자가 기본키를 설정하면서 제약 조건의 이름을 직접 지정할 수도 있음
);
```

### pk 지정과 수정
```sql
DROP TABLE IF EXISTS userTBL;
CREATE TABLE userTBL 
(   userID  CHAR(8) NOT NULL, 
    userName    VARCHAR(10) NOT NULL, 
    birthYear   INT NOT NULL
);
ALTER TABLE userTBL # 테이블 접근 변경
	ADD CONSTRAINT PK_userTBL_userID # 제약조건 추가
        PRIMARY KEY (userID); 

# 2개의 열을 합쳐 하나의 키로 써의 사용
DROP TABLE IF EXISTS prodTbl;
CREATE TABLE prodTbl
( prodCode CHAR(3) NOT NULL,
  prodID   CHAR(4)  NOT NULL,
  prodDate  DATETIME  NOT NULL,
  prodState  CHAR(10) NULL
);
ALTER TABLE prodTbl
	ADD CONSTRAINT PK_prodTbl_proCode_prodID 
	    PRIMARY KEY (prodCode, prodID) ; -- 여러 pk를 엮어서 하나의 유니크 pk로 사용

DROP TABLE IF EXISTS prodTbl;
CREATE TABLE prodTbl
( prodCode CHAR(3) NOT NULL,
  prodID   CHAR(4)  NOT NULL,
  prodDate DATETIME  NOT NULL,
  prodState  CHAR(10) NULL,
  CONSTRAINT PK_prodTbl_proCode_prodID 
	PRIMARY KEY (prodCode, prodID) 
);
```

### fk 지정과 수정
```sql
CREATE TABLE buyTBL 
(  num INT AUTO_INCREMENT NOT NULL PRIMARY KEY , 
   userID  CHAR(8) NOT NULL, 
   prodName CHAR(6) NOT NULL,
   FOREIGN KEY(userID) REFERENCES userTBL(userID)
);
DROP TABLE IF EXISTS buyTBL;
CREATE TABLE buyTBL 
(  num INT AUTO_INCREMENT NOT NULL PRIMARY KEY , 
   userID  CHAR(8) NOT NULL, 
   prodName CHAR(6) NOT NULL,
   CONSTRAINT FK_userTBL_buyTBL FOREIGN KEY(userID) REFERENCES userTBL(userID)
);
-- 제약 사항 밖으로 ALTER로 설정하기
DROP TABLE IF EXISTS buyTBL;
CREATE TABLE buyTBL 
(  num INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
   userID  CHAR(8) NOT NULL, 
   prodName CHAR(6) NOT NULL 
);
ALTER TABLE buyTBL
    ADD CONSTRAINT FK_userTBL_buyTBL 
    FOREIGN KEY (userID) 
    REFERENCES userTBL(userID);
```

### CASCADE셤 : 외래 키(Foreign Key) 제약 조건에 대한 옵션 중 하나입니다. CASCADE 옵션은 외래 키와 연관된 레코드에 대한 연쇄적인 작업을 수행하는 동작을 의미
```sql
ALTER TABLE buyTBL
    ADD CONSTRAINT FK_userTBL_buyTBL
    FOREIGN KEY (userID)
    REFERENCES userTBL (userID)
    ON UPDATE CASCADE;
```

### VIEW 임시 테이블
```sql
CREATE VIEW v_userTBL AS SELECT userID, userName, addr FROM v_userTBL;

SELECT * FROM v_userTBL;

CREATE VIEW v_userbuyTBL
AS
   SELECT U.userID AS 'USER ID', U.userName AS 'USER NAME', B.prodName AS 'PRODUCT NAME', 
		U.addr, CONCAT(U.mobile1, U.mobile2) AS 'MOBILE PHONE'
        FROM userTBL U
	        INNER JOIN buyTBL B
	            ON U.userID = B.userID;

SELECT `USER ID`, `USER NAME` FROM v_userbuyTBL; -- 주의! 백틱(키보드 1의 왼쪽 키)을 사용한다.


-- 뷰 내용 수정
ALTER VIEW v_userbuyTBL
AS
   SELECT U.userID AS '사용자 아이디', U.userName AS '이름', B.prodName AS '제품 이름', 
		U.addr, CONCAT(U.mobile1, U.mobile2)  AS '전화 번호'
      FROM userTBL U
          INNER JOIN buyTBL B
            ON U.userID = B.userID ;

SELECT `이름`,`전화 번호` FROM v_userbuyTBL; -- 주의! 백틱을 사용한다.

DROP VIEW v_userbuyTBL;

-- 에러 코드 원본 userTBL에서 BirthYear notnull 이어서 똑같이 형식상 합당하지 않음
INSERT INTO v_userTBL(userID, userName, addr) VALUES('KBM','김병만','충북') ; 
-- view 수정이 불가한 경우 1. 제약조건 2. 집계함수 사용(sum())

CREATE OR REPLACE VIEW v_sum
AS
	SELECT userID AS 'userID', SUM(price*amount) AS 'total'  
	   FROM buyTBL GROUP BY userID;
```

## 인덱스
* 클러스터형 인덱스
    - 유니크한 열에 1개만 생성 가능
    - 행 자동 정렬 
    - 무조건 NOTNULL 이여야 함
    - 참조형으로 주소안에 직접적인 값을 제어
* 보조 인덱스
    - 테이블 여러개 생성 가능
    - NULL 허용
    - 위치 주소를 가지고 값 제어

* 수정, 삭제 속도 우위 : 보조
* 검색 속도 우위 : 클러스터

```sql
CREATE TABLE userTBL -- pk는 자동으로 클러스터형 인덱스 지정을 받는다
( userID  CHAR(8) NOT NULL PRIMARY KEY, 
  userName    VARCHAR(10) NOT NULL, 
  birthYear   INT NOT NULL,  
  addr	  CHAR(2) NOT NULL,
  mobile1	CHAR(3) NULL, 
  mobile2   CHAR(8) NULL, 
  height    SMALLINT NULL, 
  mDate    DATE NULL 
);
```

```sql
CREATE TABLE  TBL2
	(	a INT PRIMARY KEY, -- 클러스터형 인덱스
		b INT UNIQUE, -- 보조 인덱스
		c INT UNIQUE, -- 보조 인덱스
		d INT 
	);
```

```sql
CREATE TABLE  TBL3
	(	a INT UNIQUE,
		b INT UNIQUE,
		c INT UNIQUE,
		d INT
	);
SHOW INDEX FROM TBL3;

CREATE TABLE  TBL4
	(	a INT UNIQUE NOT NULL,  -- 보조 인덱스
		b INT UNIQUE , -- 보조 인덱스
		c INT UNIQUE, -- 보조 인덱스
		d INT
	);
SHOW INDEX FROM TBL4;
```

```sql
CREATE TABLE  TBL5
	(	a INT UNIQUE NOT NULL, -- 보조 인덱스
		b INT UNIQUE , -- 보조 인덱스
		c INT UNIQUE, -- 보조 인덱스
		d INT PRIMARY KEY -- 클러스터형 인덱스
	);
SHOW INDEX FROM TBL5;
```

### 인덱스의 활용
```sql
CREATE UNIQUE INDEX idx_userTBL_birthYear 
    ON userTBL(birthYear)
```

## PROCEDURE
```sql
DROP PROCEDURE IF EXISTS userProc;
DELIMITER $$
CREATE PROCEDURE userProc()
BEGIN 
    SELECT * FROM userTBL;
END $$
DELIMITER $$

CALL userProc();
```

## 스토어드형 함수
```sql
DROP PROCEDURE IF EXISTS userProc1;
DELIMITER $$
CREATE PROCEDURE userProc1(IN uName VARCHAR(10))
BEGIN
    SELECT * FROM userTBL WHERE userName = uName;
END $$
DELIMITER ;

CALL userProc1('이경규');
```
```sql
DROP PROCEDURE IF EXISTS userProc2;
DELIMITER $$
    CREATE PROCEDURE userProc2(
        IN userBirth INT,
        IN userHeight INT
    )
BEGIN
    SELECT * FROM userTBL
        WHERE birthYear > userBirth AND height > userHeight;
END $$
DELIMITER ;

CALL userProc2(1970, 178);
```
```sql
DROP PROCEDURE IF EXISTS userProc3;
DELIMITER $$
CREATE PROCEDURE userProc3(
    IN txtValue CHAR(10).
    OUT outValue INT
)
BEGIN
    INSERT INTO testTBL VALUES(NULL, txtValue);
    SELECT MAX(id) INTO outValue FROM testTBL;
END $$
DELIMITER ;

CREATE TABLE IF NOT EXISTS testTBL(
    id INT AUTO_INCREMENT PRIMARY KEY, 
    txt CHAR(10)
);

CALL userProc3 ('테스트값', @myValue);
SELECT CONCAT('현재 입력된 ID 값 ==>', @myValue);
```
