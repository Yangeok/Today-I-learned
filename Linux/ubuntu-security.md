# Ubuntu 보안설정

- ssh 루트 접속 거부 및 기본 포트 변경

    ```bash
    # vi /etc/ssh/sshd_config
    Port <ssh_port>
    Protocol 2
    PermitRootLogin no
    ```

- ssh 반복 접속시 딜레이 추가

    ```bash
    apt install sshguard
    systemctl start sshguard
    ```

- 방화벽 상태 확인

    ```bash
    # using firewall-cmd
    firewall-cmd --permanent --add-port=<ssh_port>/tcp
    firewall-cmd --permanent --add-service=ssh
    firewall-cmd --reload

    # using ufw
    ufw allow ssh
    ```

- 공유 메모리에 setuid 권한 및 메모리 실행 권한 제거

    ```bash
    # vi /etc/fastab
    tmpfs /dev/shm^tmpfs^defaults,noexec,nosuid^0^0
    ```

- IP 스푸핑 공격 대비

    ```bash
    # vi /etc/sysctl.conf

    #IP  Spoofing  protection
    net.ipv4.conf.all.rp_filter = 1
    net.ipv4.conf.default.rp_filter = 1

    #Ignore  ICMP  broadcast  requests
    net.ipv4.icmp_echo_ignore_broadcasts = 1

    #Disable  source  packet  routing
    net.ipv4.conf.all.accept_source_route = 0
    net.ipv6.conf.all.accept_source_route = 0
    net.ipv4.conf.default.accept_source_route = 0
    net.ipv6.conf.default.accept_source_route = 0

    #Ignore  send  redirects
    net.ipv4.conf.all.send_redirects = 0
    net.ipv4.conf.default.send_redirects = 0

    #Block  SYN  attacks
    net.ipv4.tcp_syncookies = 1
    net.ipv4.tcp_max_syn_backlog = 2048
    net.ipv4.tcp_synack_retries = 2
    net.ipv4.tcp_syn_retries = 5

    #Log  Martians
    net.ipv4.conf.all.log_martians = 1
    net.ipv4.icmp_ignore_bogus_error_responses = 1

    #Ignore ICMP redirects
    net.ipv4.conf.all.accept_redirects = 0
    net.ipv6.conf.all.accept_redirects = 0
    net.ipv4.conf.default.accept_redirects = 0
    net.ipv6.conf.default.accept_redirects = 0

    #Ignore  Directed  pings 
    net.ipv4.icmp_echo_ignore_all = 1
    ```

- 해커가 숨겨놓은 루트킷 탐지

    ```bash
    apt install rkhunter chkrootkit
    chkrootkit
    rkhunter --update
    rkhunter --propupd
    rkhunter --check
    ```