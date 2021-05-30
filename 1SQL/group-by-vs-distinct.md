# GROUP BY과 DISTINCT 비교

- `GROUP BY`
  - 데이터를 원하는 그룹으로 나눌 수 있다.
  - 나누고자 하는 그룹의 칼럼명을 `SELECT`, `GROUP BY` 절 뒤에 추가하면 사용할 수 있다.
  - `DISTINCT`와 비슷한 용도로 집계 없이도 사용할 수 있다.
  ```sql
  -- 데이터 중복 제거
  SELECT dept_no FROM emp GROUP BY dept_no;

  -- 집계함수를 사용해 특정 그룹으로 구분하는 경우
  SELECT dept_no, MIN(sal) FROM emp GROUP BY dept_no;
  ```
- `DISTINCT`
  - 주로 중복을 제거한 칼럼을 조회하는 경우 사용한다.
  - 특정 그룹 구분없이 중복된 데이터를 제거하는 경우에 사용한다.
  ```sql
  -- 데이터 중복 제거
  SELECT DISTINCT dept_no FROM emp;

  -- 집계함수를 사용해 특정 그룹으로 구분하는 경우
  SELECT COUNT(DISTINCT d.dept_no) 'removal_duplicate', COUNT(d.dept_no) 'total_no'
  FROM emp e, dept d
  WHERE e.dept_no = dept_no;
  ```
- `HAVING`
  - `GROUP BY` 절에 거는 조건절