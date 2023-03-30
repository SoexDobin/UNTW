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

### SQL 명령어 종류

* DDL(Data Definition Language) : 데이터 정의 언어
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

* DML(Data Manipulation Language) : 데이터 조작 언어
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

* DCL(Data Control Language) : 데이터 제어 언어
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
* n:m : 하나의 데이터베이스가 여러 데이터베이스와 관계를 맺을 수 있고 반대도 가능한 다대다 관계를 의미
```
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
- ... 

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



