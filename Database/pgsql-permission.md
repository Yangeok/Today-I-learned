# pgadmin DB 접근권한 획득 및 포트 개방

- pgadmin에서 데이터베이스 접근 시도시 ident 권한이 없다고 하는 경우 사용
  - `pg_hba.conf` 파일 위치 찾기

  ```bash
  yum install mlocate
  updatedb
  locate pg_hba
  ```

  - root 계정 비밀번호 설정

  ```sql
  ALTER USER postgres WITH PASSWORD 'password';
  ```

  - 비밀번호로 로그인 설정

  ```bash
  # /var/lib/pgsql/12/data/pg_hba.conf

  # as-is
  host all all 127.0.0.1/32 peer
  # to-be
  host all all 127.0.0.1/32 md5
  ```

  - 리슨할 포트와 호스트를 설정

  ```sql
  # /var/lib/pgsql/12/data/postgres.conf

  listen_addresses = '*'
  ```

  - 서비스 재시작

  ```sql
  systemctl restart postgresql-*
  ```

- `pg_hba.conf`에서 호스트나 유저에 해당하는 아래와 같은 인증방법을 선택할 수 있다
    - `trust`: 무조건 로그인할 수 있음
    - `reject`: 무조건 로그인할 수 없음
    - `md5`: 이중 md5 해시된 패스워드를 입력해서 로그인할 수 있음
    - `password`: 암호화되지 않은 패스워드를 입력해서 로그인할 수 있음
    - `gss`: tcp/ip 연결인 경우에 gss api를 사용해서 인증할 수 있음
    - `sspi`: windows에서만 sspi를 사용해서 인증할 수 있음
    - `ident`: tcp/ip 연결인 경우에 os 사용자의 이름으로 로그인할 수 있고, 로컬 연결인 경우는 peer 인증을 사용해야 함
    - `peer`: os 사용자의 이름으로 로그인할 수 있음
    - `ldap`: ldap 서버를 사용해서 인증할 수 있음
    - `radius`: radius 서버를 사용해서 인증할 수 있음
    - `cert`: ssl 인증서로 로그인할 수 있음
    - `pam`: