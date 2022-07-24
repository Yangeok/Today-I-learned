# firewall-cmd 사용하기

- `iptables`를 래핑한 `firewalld`의 명령어 `firewall-cmd`를 아래처럼 사용할 수 있다
- 참고로 데비안 계열에서도 `ufw` 대신 `firewalld`를 사용할 수 있다
- 일반
  - `--reload`: 추가한 설정을 반영하기 위해 재시작한다
  - `—permanent`: 서비스를 재시작하고 나서도 해당 옵션이 저장되게 할때 사용한다
- 존
  - `—-get-zone`: zone 목록을 확인할 수 있다
  - `--get-default-zone`: 기본 zone 확인할 수 있다
  - `--permanent --new-zone=[존 이름]`: 새로운 zone을 확인할 수 있다
  - `--get-active-zone`: 활성화된 zone을 확인할 수 있다
  - `--list-all (--zone = [확인하고싶은 존])`: 활성화된 zone의 정보를 확인할 수 있다
- 서비스
  - `--get-services`: 존재하는 서비스 목록을 확인할 수 있다
  - `--permanent --zone=[존 이름] --add-service=[서비스명]`: zone에 서비스를 추가할 수 있다
  - `--permanent --zone=[존 이름] --remove-service=[서비스명]`: zone에 서비스를 제거할 수 있다
- 포트
  - `--permanent --zone=[존 이름] --add-port=[포트번호]/[tcp/udp]`: zone에 포트를 추가할 수 있다
  - `--permanent --zone=[존 이름] --remove-port=[포트번호]/[tcp/udp]`: zone에 포트를 제거할 수 있다
