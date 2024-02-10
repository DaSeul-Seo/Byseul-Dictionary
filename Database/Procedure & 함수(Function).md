### 💡 기준 MSSQL

## Procedure

✔️ 업무 수행 절차

> [Procedure Start]</br>
> 1.쇼핑몰 회원 로그인</br>
> 2.구매할 신발 선택</br>
> 3.개인정보 및 배송지 선택</br>
> 4.결제</br>
> [Procedure End]

- Procedure 문법

```sql
-- 프로시저 생성
CREATE OR REPLACE PROCEDURE {프로시저 이름}
     ( 매개변수명1 [ IN || OUT || INOUT ] 데이터타입,
       매개변수명2 [ IN || OUT || INOUT ] 데이터타입 ... )
IS||AS
       변수, 상수 등 선언 ( 선언부 )
BEGIN
       실행 문장 ( 실행부 )
       EXCEPTION 문장   //필수아님
END ;

```

- Procedure 예제

```sql
//사번을 입력받아 급여를 인상하는 update_sal 프로시저
CREATE OR REPLACE PROCEDURE update_sal
     ( v_empno IN NUMBER )
IS
BEGIN
       UPDATE emp
       SET sal = sal * 1.1
       WHERE empno = v_empno;
END update_sal;
```

### [프로시저의 특징]

- 'EXECUTE' or 'EXEC' 키워드로 실행

### [프로시저의 장점]

- 하나의 요청으로 여러 SQL문을 실행할 수 있다.
- 네트워크 소요시간을 줄일 수 있다.
    - 만약 동일한 쿼리를 1000번 2000번 호출하는 것보다 SP를 이용해서 구현한다면 SP를 호출할 때 한 번만 네트워크를 경유하기 때문에 네트워크 소요시간을 줄이고 성능을 개선할 수 있다.
- 개발 없무를 구분해 개발할 수 있다.
    - 순수한 애플리케이션만 개발하는 조직과 DBMS 관련 코드를 개발하는 조직이 따로 있다면, DBMS 개발하는 조직에서는 데이터베이스 관련 처리하는 SP를 만들어 API처럼 제공하고 애플리케이션 개발자는 SP를 호출해서 사용하는 형식으로 역할을 구분하여 개발이 가능하다.
- 매개변수를 받거나 전달해 줄 수 있다.

### [프로시저의 단점]

- 처리 성능이 낮다.
    - 문자나 숫자 연산에 저장 프로시저를 사용한다면 오히려 C나 JAVA보다 느린 성능을 보인다.
- 디버깅이 어렵다.
- DB 확장이 매우 힘들다.
    - 서비스 사용자가 많아져 서버수를 늘려야할 때, DB 수를 늘리는 것이 더 어렵다.
        - 서비스 확장을 위해 서버수를 늘릴경우 DB 수를 늘리는 것보다 WAS의 수를 늘리는 것이 더 효율적이기 때문에 대부분의 개발에서 DB에는 최소의 부담만 주고 대부분의 로직은 WAS에서 처리할 수 있게 한다.

## 함수(Function)

✔️ 프로시저의 각 프로세스를 수행하기 위해 필요한 기능

ex) 쇼핑몰의 로그인기능 중 ID와 PW를 체크하는 기능

- 함수문법

```sql
-- 함수생성
CREATE OR REPLACE FUNCTION {함수 이름}
     ( 매개변수명1 매개변수1타입,
       매개변수명2 매개변수2타입 ... )
RETURN 데이터타입
IS||AS
       변수, 상수 등 선언 ( 선언부 )
BEGIN
       실행 문장 ( 실행부 )
       RETURN 반환값    //필수
       EXCEPTION 문장   //필수아님
END ;
```

- 함수예제

```sql
**-- 함수 생성**
--출생년도를 입력하면 나이가 출력되는 함수
CREATE FUNCTION fn_getAge(@byear INT) -- 함수이름 fn_getAge, INT타입의 @byear를 매개변수를 1개 받음
RETURNS INT -- 함수 리턴 값은 정수형
AS
BEGIN -- 함수 시작점
	DECLARE @AGE INT -- INT타입의 @AGE라는 변수 이름 선언
	-- GETDATE()로 현재날짜를 구해서 YEAR()함수를 사용해 년도를 구하고, 
	-- @byear 매개변수 값을 빼주어 @AGE 변수 값을 세팅
	SET @AGE = YEAR(GETDATE()) - @BYEAR
	RETURN(@AGE) -- @AGE 값을 반환
END -- 함수 종료점
GO
//======================================================
--날짜를 입력하면 YYYY-MM-DD 형태로 바꿔주는 함수
CREATE OR REPLACE FUNCTION testDate ( date Date )
RETURN VARCHAR2
IS
       changeDate VARCHAR2 ( 20 ) ;
BEGIN 
       changeDate := NULL ;
       changeDate := TO_CHAR ( date, 'YYYY-MM-DD' ) ;
       RETURN changeDate ;
END ;
//======================================================
**-- 함수 호출**

```

### [함수의 특징]

- 'SELECT'로 실행

### Procedure와 함수의 차이

![1](./Img/db1.png)


### 💡 Reference
- https://runcoding.tistory.com/31
- https://mjn5027.tistory.com/47
- https://mozi.tistory.com/470
- https://lifere.tistory.com/83