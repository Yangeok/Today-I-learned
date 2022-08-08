# Zabbix trigger

- 데이터 접근이 가능한 것의 threshold를 정의한 표현식을 포함
  - e.g. `avg(/New host/system.cpu.load,3m)>2`는 3분간 cpu의 로드가 2보다 크면 트리깅된다는 의미
