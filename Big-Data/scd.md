# SCD(Slowly Changed Dimension)이란

- OLAP 환경에서 중요한 현재 시점을 기록하기 위해 사용하는 개념이다
- 데이터의 변화가 필요할 때 아래와 같이 5가지 타입을 사용한다
    - type1: 과거의 값을 없애고 현재의 값으로 직접 업데이트한다
    - type2: 행에 start, end date와 플래그를 추가한다. 팩트와 조인할 때는 start, end date로 `BETWEEN` 쿼리를 하고, flag 필드에 활성 여부를 기록한다
    - type3: 과거 기록을 새로운 prev 필드에 추가하고, 현재의 값을 직접 업데이트한다
    - type4(type1 + type3): 히스토리 테이블을 따로 만들어 type1과 같은 내용을 추가한다. 또한 대리키 필드를 하나 만든다
    - type6(type1 + type2 + type3): 짬뽕 테이블