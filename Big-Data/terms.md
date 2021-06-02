# 용어 정리

- l3 switch: ip 기준 로드밸런싱 및 라우터 역할
- hadoop
    - name node: master node. 분산 파일시스템의 네임스페이스를 관리한다. 파일이 어느 노드에 위차한 블록으로 구성되어있는지 알고 있고, 모든 변경사항을 기록한다.
    - journal node: ha를 하기 위해 사용하는 노드
    - zookeeper: race condition을 막기 위해 사용
    - hive: sql과 유사한 방식으로 하둡 데이터 접근성을 높인 솔루션
    - hue: 하둡 생태계 서비스와 그루핑하기 위한 고수준 래퍼
    - oozie: 하둡의 잡을 관리하기 위한 스케줄링 시스템
    - spark: mapReduce와 유사하고 성능이 좋다.
    - sentry: 하둡 인허가 모듈
    - impala: 대규모 병렬처리 sql 쿼리엔진
    - kerberos: 인허가 프로토콜
