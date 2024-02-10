### American National Standards Institute : 미국표준협회

### 💡 각 나라별 표준협회
- ANSI : 미국표준협회
- KS : 한국표준협회
- JIS : 일본규격협회
- DIN : 유럽

### ANSI query 특징

1. FROM 절에서 JOIN 구문 사용
2. JOIN 조건은 ON절에 명시
3. WHERE 절에는 검색조건만 명시

### ANSI query 이점

1. 표준 SQL이라 웬만한 DBMS에서 모두 인식
2. 테이블 간의 JOIN 관계가 FROM절에서 모두 기술되고, WHERE 이하 절에서는 순수하게 체크조건만 나오므로 가독성이 좋다.

### 💡 EX

```sql
--Oracle에서의 쿼리
SELECT a.ename
      ,b.ename
  FROM scott.emp a, scott.emp b
 WHERE a.mgr = b.empno
    
--ANSI SQL
SELECT a.ename
      ,b.ename
  FROM scott.emp a JOIN scott.emp b
    ON a.mgr = b.empno
```

### 💡 Reference

- https://lena19760323.tistory.com/60
- https://pyoungt.tistory.com/24