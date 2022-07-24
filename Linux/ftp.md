# ftp 사용하기

- 레드햇 계통 기준으로 `vsftpd`를 아래와 같이 설치한다

```bash
yum install -y vsftpd
```

- 서비스의 상태를 확인하고 활성화시킨다

```bash
systemctl status vsftpd
systemctl enable vsftpd
systemctl start vsftpd
```

- vsftpd를 시스템 재시작시에도 자동으로 켜지게 startup에 등록한다

```bash
chkconfig vsftpd on
```

- 방화벽을 열어주고 리로딩한다

```bash
firewall-cmd --add-service=ftp --permanent
firewall-cmd --reload
```
