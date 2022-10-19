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
	   <br>EXTRACT(MONTH FROM HIRE_DATE)  
FROM EMPLOYEE;

### DATE_FORMAT()
>날짜 포맷을 변경
- SELECT  HIRE_DATE, 
    <br>&nbsp;&nbsp;&nbsp;&nbsp;DATE_FORMAT(HIRE_DATE,'%Y%m%d%H%i%s'),
    <br>&nbsp;&nbsp;&nbsp;&nbsp;DATE_FORMAT(HIRE_DATE, '%Y/%m/%d %H:%i:%s'),
    <br>&nbsp;&nbsp;&nbsp;&nbsp;DATE_FORMAT(HIRE_DATE, '%y/%m/%d %H:%i:%s'),
    <br>&nbsp;&nbsp;&nbsp;&nbsp;DATE_FORMAT(NOW() , '%Y/%m/%d %H:%i:%s')  
FROM EMPLOYEE;

### IF(조건, 값, 값)
> 현재 근무하는 직원들의 성별을 남, 여 구분짓기
- SELECT EMP_NAME, EMP_NO,<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;IF(SUBSTR(EMP_NO,8,1) = 2, '여', '남') 성별  
FROM EMPLOYEE;

## CASE 문
> 자바의 IF, SWITCH 처럼 사용 가능

- CASE
- WHEN 조건식1 THEN 결과1
- WHEN 조건식2 THEN 결과2
- ELSE 결과3
- END

## 숫자 데이터 함수 
### ABS() : 절대값 표현
- SELECT ABS(10), ABS(-10);  

### MOD() : 주어진 컬럼이나 값을 나눈 나머지를 반환, 정수로 표현
- SELECT MOD(10,3);

### ROUND() : 지정한 자리수 부터 반올림
- SELECT ROUND(123.456, 0),		--> 0을 넣으면 소수점 첫째자리에서 반올림한다  
	   ROUND(123.456, 1),		--> 1을 넣으면 소수점 둘째자리에서 반올림한다  
	   ROUND(123.456, 2),  
	   ROUND(123.456, -2);		--> -2 넣으면 둘째자리(10의 자리)에서 반올림한다.   
	  
### CEIL() : 소수점 첫째자리에서 올림  
### FLOOR() : 소수점 이하 자리 모두 버림  
- SELECT CEIL(123.456), FLOOR(123.456);

### TRUNCATE() : 지정한 위치까지 숫자를 버리는 함수
-SELECT TRUNCATE(123.456, 0),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TRUNCATE(123.456, 1),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TRUNCATE(123.456, 2),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TRUNCATE(123.456, -2);  
	  
### CEILING() : 소수점 반올림(이라고는 하는데 올림같다)
- SELECT CEILING(4.1222);

### DATE_ADD()
### DATE_SUB()
- SELECT EMP_NAME, HIRE_DATE,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DATE_ADD(HIRE_DATE, INTERVAL 1 MONTH), 	--> HIRE_DATE + 1달  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DATE_SUB(HIRE_DATE, INTERVAL 1 YEAR)		--> HIRE_DATE - 1년  
FROM EMPLOYEE;	

### DAYOFWEEK(날짜) : 해당 날짜의 요일을 리턴
> 1: 일요일 ~ 7: 토요일
- SELECT DAYOFWEEK(NOW()); 

- SELECT EMP_NAME,  
&nbsp;&nbsp;&nbsp;CASE  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHEN DAYOFWEEK(HIRE_DATE) = 1 THEN '일요일'  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHEN DAYOFWEEK(HIRE_DATE) = 2 THEN '월요일'  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHEN DAYOFWEEK(HIRE_DATE) = 3 THEN '화요일'  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHEN DAYOFWEEK(HIRE_DATE) = 4 THEN '수요일'  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHEN DAYOFWEEK(HIRE_DATE) = 5 THEN '목요일'  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHEN DAYOFWEEK(HIRE_DATE) = 6 THEN '금요일'  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHEN DAYOFWEEK(HIRE_DATE) = 7 THEN '토요일'  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;END AS '요일'  
FROM EMPLOYEE;  
	   
- LAST_DAY(날짜) : 주어진 날짜의 마지막 일자를 조회  
SELECT LAST_DAY(NOW());

### ORDER BY 
> SELECT 통해 조회한 결과들을 특정 기준에 맞춰 정렬  
- SELECT EMP_ID, EMP_NAME 이름, SALARY, DEPT_CODE  
FROM EMPLOYEE  
- ORDER BY EMP_ID;		--> 정렬의 기본값 ASC(오름차순)  
- ORDER BY EMP_NAME ASC;  
- ORDER BY DEPT_CODE DESC, EMP_ID;	--> 일단 DEPT_CODE로 내림차순하고 그 안에서 EMP_ID 오름차순으로 정렬  
- ORDER BY 이름 DESC;  
- ORDER BY 3 DESC;	--> 컬럼의 넘버로 정렬 여기서는 SALARY를 가리키고 있다 

### GROUP BY
- 특정 컬럼이나 계산식을 하나의 그룹으로 묶어  
- 한 테이블 내에서 소그룹 별로 조회하고자 할때 선언
- 부서별 평균  
- SELECT DEPT_CODE, FLOOR(AVG(SALARY))		--> FLOOR 소수점 버려버린다  
FROM EMPLOYEE  
GROUP BY DEPT_CODE ;  

## HAVING 구문
>GROUP BY 한 각 소그룹에 대한 조건을 설정 하고자 할 때
그룹 함수와 함께 사용하는 조건 구문

## SET OPERATION 
- 합집합 (SELECT한 결과를 합친다 생각)
- UNION 
> 두 개 이상의 SELECT 한 결과(RESULT SET)를 합치는 명령어  
  중복이 있을 경우 중복되는 결과는 1번만 보여준다.
- UNION ALL 
> 두 개 이상의 SELECT 한 결과(RESULT SET)를 합치는 명령어  
중복이 있을 경우 중복이 되는 내용 그대로 조회.
- SELECT 두 개 컬럼을 잘 맞춰줘야 한다.

# JOIN --> 매우 매우 중요한 친구
> 두 개 이상의 테이블을 하나로 합쳐 사용하는 명령 구문  
 EX) DEPT_CODE 의 D5만 봤을 때 어느 부서인지 정확히 알 수 가 없는데 JOIN을 통해  
 D5가 무슨 부서인지 같이 합쳐서 가져오면 어느 부서인지 알 수 있다. 

## INNER JOIN
- 표준 SQL 방식  
SELECT DEPT_CODE, DEPT_TITLE  
FROM EMPLOYEE  
JOIN DEPARTMENT ON(DEPT_CODE = DEPT_ID)  
ORDER BY 1;  

- MYSQL 방식		  
SELECT DEPT_CODE, DEPT_TITLE  
FROM EMPLOYEE, DEPARTMENT  
WHERE DEPT_CODE = DEPT_ID;		--> JOIN을 적지않고 FROM부분에 다 적어주고 조건을 걸어서 실행  

- SELECT DEPT_CODE, DEPT_TITLE  
FROM EMPLOYEE e , DEPARTMENT d   
WHERE e.DEPT_CODE = d.DEPT_ID;		--> EMPLOYEE를 다 안적어주고 EMPLOYEE의 별명인 e를 적어서도 사용가능  

## OUTER JOIN
### LEFT JOIN
- SELECT *  
FROM EMPLOYEE e   
-- LEFT OUTER JOIN DEPARTMENT d ON(DEPT_CODE = DEPT_ID);  
LEFT JOIN DEPARTMENT d ON(DEPT_CODE = DEPT_ID);		-- OUTER 빼고 적어도 된다.  
--  LEFT OUTER JOIN : 첫번째 테이블 기준으로 두번째 테이블을 JOIN, 조건에 만족하지 않는 경우 첫번째 테이블의 값 유지

### RIGHT JOIN
- SELECT *  
FROM EMPLOYEE e   
RIGHT JOIN DEPARTMENT d ON(DEPT_CODE=DEPT_ID);  
--  RIGHT OUTER JOIN : LEFT의 반대, 두번째 테이블 기준  
-- LEFT에서는 EMPLOYEE에 D3,D4가 없어서 DAPARTMENT에 D3,D4가 삭제되었지만 RIGHT에서는 삭제 안되고 남아있다.  
-- 그리고 LEFT에서 EMPLOYEE NULL부분 살아있었지만 RIGHT에서는 삭제되었다.

#### ON() 안에는 계산식, 함수식, AND, OR 조건식 등의 표현식을 넣을 수 있다.

## SELF JOIN
> 자기 자신을 조인

- 직원의 정보와 직원을 관리하는 매니저의 정보를 조회  
SELECT EMP_ID, EMP_NAME, MANAGER_ID FROM EMPLOYEE e ;

## 다중 JOIN
> 여러 개의 테이블을 JOIN하는 것  
- 표준 SQL  
SELECT *  
FROM EMPLOYEE  
JOIN DEPARTMENT ON(DEPT_CODE = DEPT_ID)  
JOIN LOCATION ON(LOCATION_ID = LOCAL_CODE)  
JOIN JOB USING(JOB_CODE);  

- MYSQL 전용 문법  
SELECT *  
FROM EMPLOYEE, DEPARTMENT, LOCATION  
WHERE DEPT_CODE = DEPT_ID AND LOCATION_ID = LOCAL_CODE;  
-- 너무 많아지면 헷갈린다 그냥 표준 문법으로 적는게 더 직관적이고 덜 헷갈린다

## SUB QUERY
> 메인 쿼리 안에 조건이나 검색을 위한 또 하나의 쿼리를 추가하는 기법  
 쿼리안에 쿼리 --> 셀렉트문 안에 셀렉트문  

#### 단일행 서브쿼리
> 서브쿼리의 실행 결과 값이 1개 나오는 서브쿼리  
- 최소 급여를 받는 사원 정보 조회
- SELECT *  
FROM EMPLOYEE  
WHERE SALARY = (SELECT MIN(SALARY) FROM EMPLOYEE);  

#### 다중행 서브쿼리
> 결과 값이 여러 줄 나오는 서브쿼리
- 각 직급별 최소 급여를 받는 사원 정보
- SELECT *  
FROM EMPLOYEE  
WHERE SALARY IN(SELECT MIN(SALARY) FROM EMPLOYEE GROUP BY JOB_CODE);   

#### 다중행 다중열 서브쿼리
> 여러 로우, 여러 컬럼의 결과를 가져오는 서브쿼리
- SELECT *   
FROM EMPLOYEE  
WHERE (JOB_CODE, SALARY) IN(SELECT JOB_CODE, MIN(SALARY)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM EMPLOYEE  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GROUP BY JOB_CODE);

#### FROM 위치에 사용하는 서브쿼리
> Inline View(인라인 뷰)  
 테이블을 테이블명으로 직접 조회하는 대신  
 서브쿼리의 결과셋(RESULTSET)을 활용하여 데이터 조회  

 - SELECT *  
FROM (  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT EMP_ID, EMP_NAME, DEPT_TITLE, JOB_NAME  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM EMPLOYEE  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JOIN DEPARTMENT ON(DEPT_CODE = DEPT_ID)  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JOIN JOB USING(JOB_CODE)  
) T;	-- 서브쿼리의 별명(T) 꼭 설정해 줘야한다.

#### 서브쿼리의 사용 위치
- SELECT, FROM, WHERE, GROUP BY, HAVING ORDER BY
- INSERT, UPDATE, DELETE (DML)
- CREATE TABLE, CREATE VIEW (DDL)

### RANK() 
> 동일한 순번이 있을 경우 이후의 순번은 건너뛰고 메기는 함수    
1  
2  
2  
4  
- SELECT EMP_NAME, SALARY, RANK() OVER(ORDER BY SALARY DESC) 순위  
FROM EMPLOYEE;  
-- 19, 19, 21

### DENSE_RANK() 
> 동일한 순번이 있을 경우 이후 순번에 영향을 미치지 않는다  
1  
2  
2  
3  
- SELECT EMP_NAME, SALARY, DENSE_RANK() OVER(ORDER BY SALARY DESC) 순위  
FROM EMPLOYEE;  
-- 19, 19, 20

### ROW_NUMBER 
> 동일 순번은 무시.
- SELECT EMP_NAME, SALARY, ROW_NUMBER() OVER(ORDER BY SALARY DESC) 순위  
FROM EMPLOYEE;

## DDL
> CREATE : 데이터 베이스의 객체를 생성하는 DDL    
[사용형식] CREATE 객체종류 객체명 (관련 내용들...)

### CREATE TABLE
> 데이터를 저장하기 위한 틀(객체)  
데이터를 2차원의 표 형태로 담을 수 있는 객체
- CREATE TABLE MEMBER(  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MEMBER_NO INT,  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MEMBER_ID VARCHAR(20),  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MEMBER_PW VARCHAR(20),  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MEMBER_NAME VARCHAR(15)  
);

## 제약조건(CONSTRANITS)
> 테이블 생성할 때 컬럼에 값을 기록하는 것에 대한 제약사항을 설정.

- NOT NULL : 해당 컬럼에 NULL값 허용 하지 않는다.
- UNIQUE : 해당 컬럼에 중복값 허용하지 않는다.
- CHECK : 해당 컬럼에 지정한 입력사항 외에는 받지 못하게 막는다.
- PRIMARY KEY : NOT NULL + UNIQUE. 테이블 내에서 해당 행을 인식할 수 있는 고유값  EX)주민번호
- FOREIGN KEY : 다른 테이블에서 저장된 값을 연결 지어서 참조로 가져오는 데이터에 지정하는 제약조건

###  NOT NULL 제약조건 추가하여 TABLE 생성
- CREATE TABLE USER_NOT_NULL(  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_NO INT NOT NULL,   
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_ID VARCHAR(20) NOT NULL,  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_PW VARCHAR(20) NOT NULL  
);  

### UNIQUE
> 중복을 허용하지 않는 제약조건  
컬럼에 입력/수정 시 중복확인하여 중복값 있을 경우에는   
값 추가/수정 하지 못하게 막는 제약조건  
- CREATE TABLE USER_UNIQUE(  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_NO INT,  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_ID VARCHAR(20) UNIQUE,		-- 컬럼 레벨  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_PW VARCHAR(30)  
);  
- CREATE TABLE USER_UNIQUE2(  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_NO INT,  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_ID VARCHAR(20),  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_PW VARCHAR(20),  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;UNIQUE(USER_ID)				-- 테이블 레벨  
);

### UNIQUE 제약 조건을 여러 컬럼에 적용
> 1 USER01  
1 USER02  
2 USER01  
2 USER02  
- CREATE TABLE USER_UNIQUE3(  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_NO INT,  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_ID VARCHAR(20),  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_PW VARCHAR(30),  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;UNIQUE(USER_NO, USER_ID)			-- 둘 다 고려해야된다.  
);  

- INSERT INTO USER_UNIQUE3 VALUES(1, 'USER01', 'PASS01');		-- NO,ID값이 둘 중 하나만 같으면 두 가지가 동시에 같은게 아니기 때문에 정상적으로 추가된다  
- INSERT INTO USER_UNIQUE3 VALUES(1, 'USER02', 'PASS01');
- INSERT INTO USER_UNIQUE3 VALUES(2, 'USER01', 'PASS01');		-- USER01은 같지만 NO값이 다르기 때문에 정상적으로 추가된다  
- INSERT INTO USER_UNIQUE3 VALUES(2, 'USER02', 'PASS01');		-- NO값이 같지만 ID값이 다르기 때문에 정상적으로 추가된다.  
- SELECT * FROM USER_UNIQUE3;

### CHECK
> 컬럼에 값을 기록할 때 지정한 값 이외에는 값이 기록되지 않도록 범위를 제한하는 조건

- CREATE TABLE USER_CHECK(   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_NO INT,   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_ID VARCHAR(20),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;USER_PW VARCHAR(30),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ENDER VARCHAR(10) CHECK(GENDER IN('F', 'M'))  
);

- INSERT INTO USER_CHECK VALUES(1, 'USER01', 'PASS01', 'F');

- SQL Error [3819] [HY000]: Check constraint 'USER_CHECK_chk_1' is violated.  
INSERT INTO USER_CHECK VALUES(1, 'USER01', 'PASS01', 'FEMALE');

- INSERT INTO USER_CHECK VALUES(1, 'USER01', 'PASS01', 'm');		-- 정상적으로 추가가능

### CHECK 제약조건 부등호 활용
- CREATE TABLE TEST_CHECK(  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TEST_DATA INT,  
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CONSTRAINT CK_TESTCHECK_DATA CHECK(TEST_DATA > 0)  
);

INSERT INTO TEST_CHECK VALUES(10);

-- SQL Error [3819] [HY000]: Check constraint 'CK_TESTCHECK_DATA' is violated.
INSERT INTO TEST_CHECK VALUES(-10);

### CHECK 제약조건 활용 예시
- CREATE TABLE TEST_CHECK2(   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C_NAME VARCHAR(15),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C_PRICE INT,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C_DATE DATE,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C_QUAL VARCHAR(1),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CHECK(C_PRICE BETWEEN 1 AND 999999),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CHECK(C_DATE >= '2010/10/18'),  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CHECK(C_QUAL >= 'A' AND C_QUAL <= 'D')  
 );

 ### PRIMARY KEY 제약조건
- 기본키 제약조건  
- 테이블 내의 한 행에서 그 행을 식별하기 위한 고유값을 가지는 컬럼
- 해당 컬럼에 NOT NULL, UNIQUE 제약조건을 함께 걸어준다  
- 테이블 전체에 대한 각 데이터의 식별자 역할을 수행하는 제약조건  
- 기본키 제약조건은 테이블 반드시 한개만 존재해야 한다  

### FOREIGN KEY
- 외래키, 외부키, 참조키
- 다른 테이블의 컬럼값을 참조하여 참조하는 테이블의 값만을 허용한다.
- 한 테이블을 다른 테이블과 연결해주는 역할을 한다.
- FOREIGN KEY 제약조건을 통해 다른 테이블과의 관계(RELATIONSHIP)가 형성된다.
- 참조하고자 하는 컬럼은 반드시 PRIMARY KEY 이거나 UNIQUE 제약조건이 걸려 있어야 한다.


