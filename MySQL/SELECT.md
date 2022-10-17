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
- '_'&nbsp;&nbsp;  :&nbsp; _는 임의의 문자 하나
- '%' : 몇자리 문자든 관계없이 

#### ESCAPE 문자 선언.    뒤에는 특수문자가 아닌 일반문자로 선언하여 사용.

### IN 연산자
> IN (값1, 값2, 값3, ...)
- SELECT * FROM EMPLOYEE WHERE JOB_CODE IN ('J1', 'J4');  <br/> -- J1 또는 J4 인 사람들 조회
- SELECT * FROM EMPLOYEE WHERE JOB_CODE NOT IN ('J1', 'J4');<br> -- J1 또는 J4가 아닌 사람들 조회

## FUNCTION(함수)
- 문자열의 길이를 계산하는 함수
- LENGTH / CHAR_LENGTH
- LENGTH : BYTE길이 계산 (영어 1, 한글 3)
- CHAR_LENGTH : 글자 수

### INSTR : 주어진 값에서 원하는 문자가 몇번째인지 찾아 반환하는 함수
- SELECT INSTR('ABCD','A'), INSTR("ABCD",'C'), INSTR('ABCD','X'), INSTR('ABCD','BC');

### SUBSTR : 주어진 문자열에서 특정 부분만 꺼내오는 함수
- SELECT 'HELLO WORLD',  
		SUBSTR('HELLO WORLD',1,5),&nbsp;&nbsp;&nbsp;-- 1~5 문자들 가져온다  
		SUBSTR('HELLO WORLD',7);&nbsp;&nbsp;&nbsp;-- 7번째 문자부터 가져온다

### LPAD / RPAD
> 빈칸을 지정한 문자로 채우는 함수
- SELECT __LPAD__(EMAIL, 20, '*') 	--> 이메일을 가져오는데 20칸 짜리 공간을 만들고 비는 공간은 * 채운다는 소리  
FROM EMPLOYEE;  
- SELECT __RPAD__(EMAIL, 20, '*') 	--> LPAD는 왼쪽 공간에 채워넣고, RPAD는 오른쪽 공간에 채워넣은다.   
FROM EMPLOYEE;

### LTRIM / RTRIM : 공백 제거 
- SELECT LTRIM(' &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HELLO');	--> 문자열 왼쪽 공백 제거
- SELECT RTRIM('HELLO&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'); --> 문자열 오른쪽 공백 제거

### TRIM : 양끝을 기준으로 특정 문자를 지워주는 함수
- SELECT TRIM('&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2교시&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;');
- SELECT TRIM('0' FROM '000123000');&nbsp;&nbsp;&nbsp;&nbsp;--> 앞,뒤 공백뿐만 아니라 특정 문자도 지워준다
- SELECT TRIM('0' FROM '&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;000123000');	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> 0을 만나기 전에 공백을 만나버려서 바로 끝나버린다

### CONCAT : 여러 문자열을 하나로 합치는 함수
- SELECT CONCAT('마이에스큐엘', ' 너무너무너무 재밌어요 :)');

### REPLACE
- SELECT REPLACE('HELLO WORLD', 'HELLO', 'BYE');&nbsp;&nbsp;&nbsp;&nbsp;--> HELLO를 찾아서 BYE로 바꿔준다
- SELECT REPLACE('HELLO WORLD', 'ELLO', 'BYE');	&nbsp;&nbsp;&nbsp;&nbsp;--> HBYE로 바뀐다

#### 단일행함수 : 각 행마다 함수 적용
#### 다중행함수 : 조건에 만족하는 모든 행을 찾고 한번에 연산
#### 그룹함수 : SUM, AVG, MAX, MIN, COUNT

### SUM(컬럼)
- SELECT SUM(SALARY) FROM EMPLOYEE;

### AVG(' ')
- SELECT AVG(SALARY) FROM EMPLOYEE;

### MAX(), MIN()
- SELECT MAX(SALARY), MIN(SALARY)  
FROM EMPLOYEE;

### COUNT() : 행의 갯수
- SELECT COUNT(*), COUNT(DEPT_CODE), COUNT(DISTINCT DEPT_CODE)   
FROM EMPLOYEE;

### SYSDATE(), NOW() : 현재 컴퓨터의 날짜를 반환
- SELECT SYSDATE(), NOW() ;
> NOW()와 SYSDATE()의 차이는 쿼리가 길어질 경우, 출력 되는 시간이 고정되느냐 변하느냐에 따른 차이가 있다.  
NOW 는 쿼리가 처음 시작되는 시간이 고정되지만 SYSDATE 는 연산할 때 마다 시간이 변합니다.

### 두 날짜 사이의 차
> DATEDIFF : 단순 일 차이  
> TIMESTAMPDIFF : 연, 분기, 월, 주, 일, 시, 분, 초 지정하여 차이
- SELECT HIRE_DATE 입사일, DATEDIFF(NOW(), HIRE_DATE)+1  
FROM EMPLOYEE;

- SELECT EMP_NAME, HIRE_DATE, TIMESTAMPDIFF(YEAR, HIRE_DATE, NOW())  
FROM EMPLOYEE;

### EXTRACT : (YEAR | MONTH | DAY FROM 날짜데이터) : 지정한 날로부터 날짜 값을 추출
- SELECT HIRE_DATE, EXTRACT(YEAR FROM HIRE_DATE),
	   EXTRACT(MONTH FROM HIRE_DATE)  
FROM EMPLOYEE;