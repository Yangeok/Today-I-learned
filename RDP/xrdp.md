# xrdp로 원격 데스크탑 접속

- 원격 데스크톱을 제공할 서버에 xrdp 서비스가 실행되고 있고, 포트가 열렸는지 확인
- 접속할 서버가 windows라면
    - [https://harryp.tistory.com/162](https://harryp.tistory.com/162)
    - 내컴퓨터 우클릭 -> 설정 -> 고급 시스템 설정 -> 원격 -> `원격 데스크톱`의 설정을 `연결 허용`으로 변경
    - rdesktop 실행

        ```dart
        $ rdesktop 192.168.0.3 -g 1600x900 -u parkch0708
        ```

- macos라면
    - app store에서 microsoft remote desktop 다운로드
    - ssh로 접속하는 방법과 똑같이 호스트 설정
    - ssh 사용자, 비밀번호를 입력하면 데스크톱 실행