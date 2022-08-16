# Oracle Tablespace와 테이블 파티셔닝 방법

- tablespace: 프로시져, 테이블, 뷰 등을 논리적으로 나눈 공간
- datafile: 데이터를 물리적으로 나눈 공간

## 파티셔닝 방법

- Range
  - 특정 기준을 가지고 범위를 나누는 방법 (e.g. 날짜)
  - 데이터가 균일하게 분포되지 못해 성능 저하를 초래할 수 있음
- Hash
  - hash 함수가 데이터를 파티션 별로 균등하게 배분 (like 로드밸런서)
  - 사용자는 특정 데이터가 어떤 파티션에 저장되는지 알 수 없음
  - 성능은 좋지만 관리하기 어려운 단점이 있음
  - 파티션이 지정되지 않은 값을 입력하면 에러가 발생함
- List
  - 파티셔닝할 항목을 운영자가 직접 지정하는 방식
  - `DEFAULT` 파티션을 생성해야 함
  - 새로운 list 파티션을 추가해야 하는 경우, 기존 `DEFAULT` 파티션을 삭제 후 새로운 파티션을 생성해야 함
- Composite
  - Range-Hash: 선 Range 후 Hash
  - Range-List: 각 레코드가 어느 파티션에 속할지 알 수 있지만, 구문이 장황해짐
  - Range-Range, List-Range, List-List, List-Hash
- Interval
  - 파티션 범위를 넘어간 데이터는 에러로 입력되지 않음 (~10g)
  - 스스로 파티션을 생성함 (11g)
  - `numToYMinterval(int, separator[DAY, HOUR, MINUTE, SECOND])`로 파티션을 생성함
- System
  - 파티션 키를 파티션 생성시 지정하지 않고, 데이터 삽입할 때 직접 지정하는 방식
