# Oracle Tablespace

- 정의
  - datafile라는 이름의 물리 파일로 데이터를 저장함
  - datafile 하나 이상이 모여 tablespace라는 논리적 저장공간을 형성함
  - 하나의 데이터베이스 안에 가장 큰 논리적 저장공간
  - 업무의 단위에 따라 여러 개로 분리할 수 있음
  - segment라는 논리적 저장공간의 집합
  - 용량이 가득차면 오라클 서비스가 중단됨
  - 따로 설정하지 않은 경우 테이블 생성시 자동으로 tablespace를 연결함
- 종류
  - permanent
    - 가장 일반적인 형태로 쓰임
    - 고의적으로 삭제하지 않는 한 영구적으로 보존되는 객체를 저장하기 위한 용도
    - 임의의 이름을 지정하여 데이터를 저장할 수 있음
    - `SYSTEM`, `SYSAUX`가 기본으로 할당되어 있음
      - `SYSTEM`: Data Dictionary Table이 저장되는 공간
      - `SYSAUX`: `SYSTEM`의 보조 역할로 `SYSTEM`의 유틸리티/함수를 저장한 공간
  - undo
    - 읽기에 일관성을 유지하기 위해 사용함
    - DML이 실패한 경우 롤백하기 위해 수정 이전의 값을 이 곳에 저장함
    - 데이터베이스 운영을 위해 적어도 하나의 Undo가 필요함
  - temporary
    - 사용자 쿼리 요청으로 정렬작업이 필요할 떄 메모리 부하를 줄이기 위해 사용
- 구문
  - 조회

    ```sql
    SELECT TABLESPACE_NAME, CONTENTS FROM DBA_TABLESPACES
    ```

  - 생성

    ```sql
    CREATE TABLESPACE <tablespace_name>
    DATAFILE <file_path>
    SIZE <init_file_size>
    AUTOEXTEND ON NEXT <extend_size> -- 초기 크기 공간을 모두 사용하는 경우 자동으로 파일 크기를 증량
    MAXSIZE <max_size> -- 기본값 무제한
    UNIFORM SIZE <size> -- extent 한개의 크기
    ```

  - 수정
    - 연결된 테이블 변경

      ```sql
      ALTER TABLE <talbe_name> MOVE TABLESPACE <tablespace_name>
      ```

    - 속성 변경
      - 물리적 파일의 위치/이름 변경

        ```sql
        ALTER TABLESPACE RENAME <a> to <b>
        ```

      - 용량 변경

        ```sql
        ALTER TABLESPACE <tablespace_name> ADD DATAFILE <file_name> SIZE <size>
        ```

      - 기존 파일에 용량이 꽉차는 경우 자동 용량 증가

        ```sql
        ALTER DATABASE DATAFILE <file_path> AUTOEXTEND ON NEXT <size> MAXSIZE <size>
        ```

  - 삭제
    - 테이블, 인덱스 등 객체를 모두 삭제

    ```sql
    DROP TABLESPACE <tablespace_name> INCLUDE CONTENTS
    ```

    - 데이터가 있는 tablespace를 제외한 모든 segment 삭제

    ```sql
    DROP TABLESPACE <tablespace_name> INCLUDING CONTENTS
    ```

    - 다른 tablespace에 연결된 제약조건을 포함 삭제

    ```sql
    DROP TABLESPACE <tablespace_name> CASCADE CONSTRAINTS
    ```

    - tablespace의 물리파일 포함 삭제

    ```sql
    DROP TABLESPACE <tablespace_name> INCLUDING CONTENTS AND DATAFIELS
    ```
