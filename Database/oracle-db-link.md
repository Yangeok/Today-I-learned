# Oracle database link

- `*lob`이 포함된 데이터를 옮기기에 데이터를 덤핑하는 것은 적절한 방법이 아님
  - csv의 경우 바이너리가 포함되어 `,`를 사용할 수 없음
  - sql의 경우 `*lob`이 16진수로 표기되어 쿼리 실행시간이 길어짐
- 링크
  - 현재 DB에서 네트워크상 다른 DB에 접속하기 위한 설정을 정의하는 객체
  - 호스트명과 SID가 달라야 연결 가능
  - 문자열집합이 같아야 연결 가능하고, 문자열집합이 다른경우 `????`로 데이터가 표기됨
  - 구문
    - `public`
    - `link_name`
    - `service_name`
    - `username`, `password`
  - 사용 예시
    - 다음과 같이 링크를 연다

    ```sql
    CREATE DATABASE LINK <link_name>
    CONNECT TO <username> IDENTIFIED BY "<password>"
    USING '<service_name>';
    
    -- or
    USING '
      (DESCRIPTION=
        (ADDRESS=(PROTOCOL=TCP)(HOST=<host_name>)(PORT=<port>))
        (CONNECT_DATA=(SERVICE_NAME=<sid>))
      )
    ';
    ```

    - 링크를 닫을 때는 다음과 같이 한다

    ```sql
    DROP DATABASE LINK <link_name>;
    ```

    - 링크를 열고 원하는 쿼리를 하되 `*lob`이 포함된 경우 다음과 같은 트릭을 사용한다

    ```sql
    INSERT INTO <db_name>.<table_name> /*+ append nologging */ 
    SELECT * 
    FROM <db_name>.<table_name>@<link_name>;
    ```

    - `tnsnames.ora`에 연결 문자열이 정의되어 있어야 alias 사용이 가능
