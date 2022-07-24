# Zabbix active vs. passive

- 에이전트는 로컬 동작 정보를 모아서 zabbix-server에 데이터를 보낸다
- zabbix-agent가 설치된 서버에서 에이전트들은 다음 체크가 모두 가능하다
  - passive (pull 방식)
    - 에이전트가 데이터 요청에 응답한다
  - active (push 방식)
    - passive 방식에 비해 복잡한 과정이 필요하다
    - 서버로부터 미리 아이템 리스트를 받는다
    - 주기적으로 아이템별 생성된 값을 서버로 보낸다 (`10051` 포트 사용)
    - 에이전트별 설정파일에서 `ServerActive=*`을 설정해줘야 한다
