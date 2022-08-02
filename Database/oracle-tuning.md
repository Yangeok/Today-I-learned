# 오라클 튜닝

## 쿼리 최적화

- 함수 사용으로 반복 테이블 스캔 제거

  ```sql
  -- before
  SELECT A.AGENT_NO, A.YYYYMM, MIN(A.SALE_AMT), SUM(B.SALE_AMT)
  FROM TB_SALE_MONTH A, TB_SALE_MONTH B
  WHERE A.YYYYMM >= B.YYYYMM
  AND A.AGENT_NO = B.AGENT_NO
  GROUP BY A.AGENT_NO, A.YYYYMM
  ORDER BY A.AGENT_NO, A.YYYYMM;

  -- after
  SELECT AGENT_NO, YYYYMM, SALE_AMT, 
    SUM(SALE_AMT) OVER (
      PARTITION BY AGENT_NO 
      ORDER BY AGENT_NO, YYYYMM
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    )
  FROM TB_SALE_MONTH;
  ```

- 재귀 호출 최소화

  ```sql
  -- before
  FROM (
    SELECT EMP_NO, EMP_NM, DEPT_NO, 
      FN_GET_EMP_CNT(DEPT_NO) EMP_CNT
    FROM TB_EMP
  ) A

  -- after
  FROM (
    SELECT EMP_NO, EMP_NM, DEPT_NO, 
      (
        SELECT FN_GET_EMP_CNT(DEPT_NO)
        FROM DUAL
      )
    FROM TB_EMP
  ) A
  ```

- `OUTER JOIN`을 서브쿼리 형태로 변경 (스칼라 서브쿼리)
- 인라인 뷰를 사용한 해시 조인으로 성능 개선

  ```sql
  -- before
  FROM TB_PRDT_SALE_DAY A, TB_PRDT B -- 1:M 관계
  WHERE A.SALE_DT BETWEEN '20200101' AND '20200130'
    AND A.PRDT_CD = B.PRDT_CD
  GROUP BY A.PRDT_CD;

  -- after
  FROM ( -- 1:1 관계로 치환
    SELECT A.PRDT_CD, SUM(A.SALE_CNT) SALE_CNT_SUM, SUM(A.SALE_AMT) SALE_AMT_SUM
    FROM TB_PRDT_SALE_DAY A
    WHERE A.SALE_DT BETWEEN '20200101' AND '20200130'
    GROUP BY A.PRDT_CD
  ) A,
  TB_PRDT B
  WHERE A.PRDT_CD = B.PRDT_CD
  ```

- 정렬이나 해시 작업을 최소화

## 엔진 최적화

- 적절한 인덱스로 블록 I/O 최적화
  
  ```sql
  -- before
  CREATE INDEX TB_ORD_IDX01 ON TB_ORD(ORD_DT, ORD_NM);
  
  -- after
  CREATE INDEX TB_ORD_IDX01 ON TB_CUST(CUST_NM);
  CREATE INDEX TB_ORD_IDX02 ON TB_ORD(ORD_DT, ORD_NM);
  ```
