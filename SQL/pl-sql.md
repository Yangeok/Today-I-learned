# PL/SQL

- Procedural Language extension to SQL
- 의미
  - SQL을 확장한 절차적 언어
  - 여러 SQL을 한 블럭으로 구성해 commit, rollback, try/except 등을 제어할 수 있음
  - 커서를 사용해 대용량 처리시 분할 처리 가능
  - 조건/반복문을 사용한 프로그래밍 가능
  - 동적으로 문자열로 작성한 SQL을 실행할 수 있음
- 기본 구조
  - `DECLARE`, `BEGIN`, `EXCEPTION`, `END`가 한 블럭을 이룸
  - 한 블럭은 `BEGIN`과 `END` 사이 여러번 사용할 수 있음
  - `DECLARE`로 변수를 선언할 수 있음
