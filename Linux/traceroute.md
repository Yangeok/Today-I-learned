# traceroute 사용법

- 목적지까지 네트워크 상태를 체크하는 `ping`, 목적지의 애플리케이션이 살아있는지 체크하는 `telnet`도 동작하지 않을 때 출발지와 목적지 사이 모든 라우터를 추적하는 `traceroute`를 사용할 수 있다
- `ping`과 동일하게 icmp 프로토콜을 사용해 패킷을 추적한다
- 사용 목적
  - 네트워크에서 데이터 손실이 일어날 때 문제가 있는 노드를 체크하는 경우 사용한다
  - 네트워크 트래픽에 병목이 생긴 구간을 확인하기 위해 사용한다
- 옵션
  - `-m`: 홉 갯수 (거치는 라우터 수)
  - `-n`: 호스트명 찾기 비활성화
  - `-w`: 타임아웃
