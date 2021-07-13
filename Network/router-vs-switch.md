# 스위치 vs. 라우터

- 스위치
    - 데이터 링크 계층에 속한다
    - 맥 주소를 기반으로 작동한다
    - 브로드캐스트 도메인을 구분할 수 없다
    - 자신에게 들어온 데이터의 목적지가 불분명하고, 모든 포트로 데이터를 퍼뜨리는 브로드캐스팅을 한다
    - 학습기능이 있어 별도 설정 없이도 사용가능하다
    - L3 스위치는 라우터와 같은 계층 역할을 수행한다
- 라우터
    - 네트워크 계층에 속한다
    - IP 주소를 기반으로 작동한다
    - 브로드캐스트 도메인을 구분할 수 있어서, 포트별로 서로 다른 네트워크 대역을 연결할 수 있다
    - 데이터의 목적지가 불분명하다면 데이터를 버린다
    - 설정이 있어야 라우팅 테이블 생성 및 통신이 가능하다