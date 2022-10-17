## SELECT 문
- SELECT  : 조회용 SQL 문장
- SELECT *(조회용 컬럼)	: 조회하고자 하는 내용
- FROM 테이블명			: 조회하고자 하는 테이블
- [WHERE 조건] 			: 특정 조건
- [ORDER BY 컬럼]		: 정렬

### 현재 DATABASE가 가진 모든 테이블 출력
- SHOW TABLES;

### 모든 행과 모든 컬럼 조회
- SELECT * FROM EMPLOYEE;

### 모든 사원의 ID와 사원명, 연락처를 조회
- SELECT EMP_ID, EMP_NAME, PHONE FROM EMPLOYEE;

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

### 컬럼값을 사용해서 계산식을 적용한 정보 조회  		(컬럼값이 NULL이면 어떤계산을 해도 NULL로 나온다)
- SELECT EMP_NAME "사원명", (SALARY * 12) "연봉", BONUS 보너스, (SALARY+(SALARY*BONUS))*12 "연봉총합"  
FROM EMPLOYEE;

### IFNULL() : 만약 현재 조회한 값이 NULL일 경우 지정한 값으로 변경
- SELECT BONUS 보너스, IFNULL(BONUS,0)  -- BONUS 가져올때 값이 NULL이면 0으로 가져온다  
FROM EMPLOYEE;

### DISTINCT : 중복 제거하고 한개만 조회
- SELECT DISTINCT DEPT_CODE  
FROM EMPLOYEE;

## 연산자
- 비교연산자
- <, >, <=, >= : 크기를 나타내는 부등호
-  = : 같다
-  !=, <> : 같지 않다

### 급여가 350만원 이상, 550만원 이하인 직원의 사번, 사원명, 부서코드, 직급코드, 급여정보 조회
>  BETWEEN A AND B  
- SELECT EMP_ID 사번, EMP_NAME 사원명, DEPT_CODE 부서코드, JOB_CODE 직급코드, SALARY 급여   
FROM EMPLOYEE  
WHERE SALARY BETWEEN 3500000 AND 5500000;

## LIKE
- 해당하는 숫자나 문자가 포함된 정보를 조회할 때 사용하는 연산자
- '_' : _는 임의의 문자 하나
- '%' : 몇자리 문자든 관계없이