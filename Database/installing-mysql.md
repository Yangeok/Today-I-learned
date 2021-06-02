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

- mariadb와 충돌 생기는 경우
```jsx
Error: Package: akonadi-mysql-1.9.2-4.el7.x86_64 (@anaconda)
           Requires: mariadb-server
           Removing: 1:mariadb-server-5.5.60-1.el7_5.x86_64 (@updates)
               mariadb-server = 1:5.5.60-1.el7_5
           Obsoleted By: mysql-community-server-8.0.13-1.el7.x86_64 (mysql80-community)
               Not found
           Available: 1:mariadb-server-5.5.56-2.el7.x86_64 (base)
               mariadb-server = 1:5.5.56-2.el7
```
- 아래와 같이 mariadb를 삭제하면 에러를 해결할 수 있다
```jsx
yum -y remove mariadb-libs
```