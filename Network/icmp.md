# ICMP란

- Internet Control Message Protocol
- 유래
  - 3계층의 IP 프로토콜은 전송상태에 대한 관리가 이뤄지지 않는 신뢰할 수 없는 프로토콜이다.
  - IP 프로톸ㄹ의 단점을 보완하기 위해 생긴 프로토콜이다.
- 용도
  - 일반적인 상황이나 오류 보고
- 기능
  - IP를 이용해 메시지 전달
  - 네트워크(L3) 계층에 속함
- 활용
  - ping 명령어를 통해 상대 호스트의 작동 여부나 응답시간을 측정하는데 사용한다
  - 윈도우즈에서 tracert 명령어를 통해 목적지까지 라우팅 경로 추적을 위해 사용한다
- 구조
  - Type: icmp 메시지의 유형과 용도를 표현함 (8bit)
  - Code: Type의 세부내용으로 Type과 Code가 조합되어 icmp 메시지의 용도와 목적을 나타냄 (8bit)
  - Checksum: icmp 메시지의 오류를 검사하기 위한 값 (16bit)
  - Rest of the header: Type과 Code에 따라 추가되는 헤더
  - Data section: 데이터가 위치하는 영역
- 에러 리포팅 메시지
  - Destination Unreachable (Type 3)
    - Code 1 (Host Unreachable): 최종 단계의 라우터가 목적지 호스트로 패킷전송에 실패한 경우
    - Code 2 (Protocol Unreachable): 목적지 호스트에서 특정 프로토콜을 사용할 수 없는 경우
    - Code 3 (Port Unreachable): 목적지 호스트에 해당 udp 포트가 열려있지 않는 경우
    - Code 4 (Fragmentation needed and don't fragment was set): ip 헤더의 Don't fragment 플래그가 설정되어 단편화할 수 없는 경우 반환함
  - Redirection (Type 5)
    - 라우팅 경로가 잘못되어 새로운 경로 이전 경유지 혹은 호스트에게 알려주는 메시지
    - icmp redirect 공격시 이용하는 메시지
  - Time Exceeded (Type 11)
    - Code 0 (Time To Live exceeded in Transit): ip 패킷이 최종 목적지에 도달하기 전에 ttl 값이 0이 되어 해당 패킷이 폐기되는 경우
    - Code 1 (Fragment reassembly time exceeded): ip 패킷 재조합 과정에서 타임아웃이 발생해 goekd vozltdl vPrlehlsms ruddn
