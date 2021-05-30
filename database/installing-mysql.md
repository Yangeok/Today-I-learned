# CentOS에서 MySQL 설치

- community, commercial 버전 모두 설치방법은 똑같음
- 설치 후 서비스에 등록 및 실행

```bash
$ systemctl start mysqld
$ systemctl status mysqld
$ systemctl enable mysqld
```

- 기본 비밀번호 찾기

```bash
$ grep 'temporary password' /var/log/mysqld.log
2021-05-24T02:37:05.065388Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: l,rcqgPdr1Lu
```

- 비밀번호 변경하기

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'NEW_PASSWORD';
Query OK, 0 rows affected (0.04 sec)
```

- 방화벽 설정하기

```bash
$ firewall-cmd --permanent --zone=public --add-port=3306/tcp
$ vi /etc/firewalld/zones/public.xml
$ systemctl restart firewalld
```