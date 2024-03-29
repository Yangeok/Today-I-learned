# Lock

- 의미
  - 트랜잭션 처리에 순차성을 부여하기 위한 방법
- 종류
  - shared(=read)
    - 데이터를 읽을 때 사용됨
    - 공유락끼리는 동시에 접근이 가능
    - 하나의 데이터를 읽는 것은 여러 사용자가 동시에 할 수 있음
    - 공유락이 설정된 데이터에 배타락을 사용할 수 없음
  - exclusive(=write)
    - 데이터를 변경할 때 사용됨
    - 트랜잭션이 완료될 때까지 유지됨
    - 배타락이 해제될 때까지 다른 트랜잭션(읽기 포함)은 해당 데이터에 접근할 수 없음
- 범위
  - 데이터베이스
    - 1개 세션만 DB 데이터에 접근 가능
    - 일반적으로 사용하지 않음
    - 소프트웨어 버전을 올리거나 주요 DB 업데이트시 사용함
  - 파일
    - 테이블/레코드 등과 같은 실제 데이터를 쓰는 물리적인 저장소
    - 일반적으로 사용하지 않음
  - 테이블
    - 테이블의 모든 행을 업데이트하는 등 전체 테이블에 영향을 주는 변경을 수행할 때 유용함
    - DDL 구문과 함께 사용하여 DDL락이라고 함
  - 페이지/블럭
    - 파일의 일부인 페이지/블록을 기준으로 설정
    - 일반적으로 사용하지 않음
  - 칼럼
    - 락 설정/해제에 리소스가 많이 소모됨
    - 일반적으로 사용하지 않음
  - 행
    - DML 구문과 함께 사용함
    - 가장 일반적으로 사용하는 락
- 블로킹
  - 의미
    - 락간(배타-배타/배타-공유)에 경합조건이 생겨 멈춘 상태
    - 블로킹을 해소하기 위해 트랜잭션이 완료되어야 함
    - 뒤의 트랜잭션은 이전 트랜잭션이 마무리되어야 진행이 가능함
    - 경합조건은 성능에 악영향을 미치기때문에 경합을 최소화시킬 필요가 있음
  - 주의사항
    - 한 트랜잭션의 길이가 너무 긴 경우 경합 확률이 증가함
    - 데이터를 갱신하는 트랜잭션이 동시에 수행되지 않도록 설계 필요
    - 트랜잭션 경리 수준을 불필요하게 상향 조정하지 않기
    - 쿼리를 오랜시간 잡지 않도록 적절한 튜닝을 진행
- 교착상태
  - 두 트랜잭션이 각각 락을 접근하고 서로 락에 접근하여 값을 얻어오려고 할 때 발생
  - 양쪽 트랜잭션 모두 영원히 처리되지 않는 상태
  - 교착상태 발생시 둘 중 한 트랜잭션에 에러를 발생시켜서 문제를 해결함
  - 교착상태 발생 가능성을 줄이기 위해 접근 순서를 동일하게 하는 것이 중요
