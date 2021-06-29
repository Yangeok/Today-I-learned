# 게이트웨이 vs. 라우터

- 게이트웨이와 라우터는 비슷한 개념이다
- 소프트웨어 측면에서는 게이트웨이라고 한다
- 하드웨어 측면에서는 라우터라고 한다
- LAN 영역 간 호스트와 호스트 사이를 연결하는 역할을 라우터가 하며, 이것을 라우팅이라고 한다
- 서브넷 마스크의 `255`인 부분에 해당하는 네트워크 ID는 LAN 영역 간을 구분할 때 사용한다
- 서브넷 마스크의 `0`인 부분에 해당하는 호스트 ID는 동일 네트워크 영역 내 호스트끼리 구분할 때 사용한다
- 출발지와 목적지의 네트워크 ID가 다른 경우는 다른 LAN 영역에 있고, 라우팅이 필요하다
- 출발지와 목적지의 네트워크 ID가 동일한 경우는 같은 LAN 영역에 있고, 스위칭이 필요하다