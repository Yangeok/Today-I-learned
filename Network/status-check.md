# 상태 확인하기

- ping
    - ICMP(Internet Control Message Protocol) 에코 요청을 목적지에 보내고 응답을 받아서 네트워크 상태를 확인한다
    - IP나 도메인으로 확인할 수 있다

    ```bash
    ping localhost

    PING localhost (127.0.0.1): 56 data bytes
    64 bytes from 127.0.0.1: icmp_seq=0 ttl=64 time=0.088 ms
    64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.179 ms
    ^C
    --- localhost ping statistics ---
    2 packets transmitted, 2 packets received, 0.0% packet loss
    round-trip min/avg/max/stddev = 0.088/0.134/0.179/0.045 ms
    ```

    - `64 bytes from 127.0.0.1`: 루프백인 로컬호스트에서 64 바이트의 응답을 함
    - `icmp_seq=1`: 1번째 ICMP(ping) 신호, 숫자는 패킷의 일련번호
    - `ttl=64`: time to live라고도 하며, 몇 개의 다리를 건너 통신했는지를 알려준다
        - 64는 1개의 다리도 건너지 않았다는 뜻
        - 55는 9개의 큰 다리를 건너 통신한다는 뜻
    - `time=0.088 ms`: 요청한 서버와의 통신 시간을 말한다
    - `2 packets trasmitted, 2 packets received, 0.0% packet loss`: 패킷을 보내고 받은 수, 손실률을 말한다
    - `rount-trip /min/avg/max/stddev`: time의 최소값, 평균값, 최대값, 표준편차를 말한다
- traceroute
    - 통신이 어떻게 일어나는지를 알려주며, ping과 같이 ICMP를 사용한다
    - UDP로 요청하고 ICMP로 응답을 받는다
    - IP나 도메인으로 확인할 수 있다

    ```bash
    traceroute 8.8.8.8

    traceroute to 8.8.8.8 (8.8.8.8), 64 hops max, 52 byte packets
     1  192.168.0.1 (192.168.0.1)  14.295 ms  8.124 ms  3.418 ms
     2  211.108.*.* (211.108.*.*)  5.196 ms  4.046 ms  5.896 ms
    ```

    - 중간에 `* * *`로 뜨는 구간은 해당 네트워크 장비가 ICMP를 허용하지 않은 경우이다
    - TTL 값을 1부터 시작해서 1개씩 올려가면서 알아가므로 시간이 ping보다 더 오래 걸린다
    - 특정 서버와 통신이 안될 때 어디 구간에서 안되는지 파악하는데 도움이 된다
- nmap
    - 원격지 서버의 어떤 포트가 열려있는지 확인할 수 있다
    - 운영체제가 무엇인지까지도 알 수 있다
    - 다음은 루프백으로 nmap을 날린 결과이다

    ```bash
    nmap localhost

    Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-04 12:32 KST
    Nmap scan report for localhost (127.0.0.1)
    Host is up (0.00038s latency).
    Other addresses for localhost (not scanned): ::1
    Not shown: 995 closed ports
    PORT     STATE    SERVICE
    1080/tcp open     socks
    1087/tcp open     cplscrambler-in
    1105/tcp filtered ftranhc
    5432/tcp open     postgresql
    8081/tcp open     blackice-icecap
    ```

    - 다음은 로컬 IP로 nmap을 날린 결과이다

    ```bash
    nmap 192.168.0.7

    Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-04 12:38 KST
    Nmap scan report for 192.168.0.7
    Host is up (0.00028s latency).
    Not shown: 998 closed ports
    PORT     STATE SERVICE
    5432/tcp open  postgresql
    8081/tcp open  blackice-iceca
    ```

    - 어떤 포트가 내부에만 열려있고, 외부로 공개되어있는지를 확인할 수 있다
    - 실제로 프로세스가 작동해서 해당 포트를 열어두고 있는지, 방화벽에서 막히지 않았는지 확인할 수 있는 가장 좋은 방법인 nmap이다