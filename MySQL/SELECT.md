## SELECT 문
- SELECT  : 조회용 SQL 문장
- SELECT *(조회용 컬럼)	: 조회하고자 하는 내용
- FROM 테이블명			: 조회하고자 하는 테이블
- [WHERE 조건] 			: 특정 조건
- [ORDER BY 컬럼]		: 정렬

### 현재 DATABASE가 가진 모든 테이블 출력
> SHOW TABLES;

### 모든 행과 모든 컬럼 조회
> SELECT * FROM EMPLOYEE;

### 모든 사원의 ID와 사원명, 연락처를 조회
>  SELECT EMP_ID, EMP_NAME, PHONE FROM EMPLOYEE;

## WHERE 구문
- 테이블에서 조건을 만족하는 값을 가진 행을 따로 선택하여 조회하는 조건절
- 여러개의 조건을 선택하고 할 경우에는 AND | OR 명령어를 함께 사용

## 컬럼에 별칭 달기
1. AS 표현
SELECT  EMP_ID AS "사원번호", EMP_NAME AS 사원명	--> "" 안해도 나온다  
FROM EMPLOYEE;

2. AS 생략
SELECT EMP_ID "사원번호()", EMP_NAME '사원 명', EMAIL 이메일		--> 띄어쓰기나 ()를 쓸때는 "",'' 생략하면 안된다  
FROM EMPLOYEE;

