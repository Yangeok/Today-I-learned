# Dockerfile 명령어

- `FROM`: 베이스 이미지
- `ARG`: 내부 변수 혹은 docker-compose 파일을 사용하는 경우 주입된 변수
- `RUN`: 이미지를 빌드할 때 실행할 명령

    ```docker
    RUN apt-get -y update                           # Shell 형식
    RUN ["/bin/bash", "-c", "apt-get -y update"]    # Exec 형식
    ```

    - 패키지나 미들웨어를 설치할 때 사용한다
    - exec 형식이 권장된다
- `CMD`: 컨테이너를 구동할 때 실행할 명령

    ```docker
    CMD echo "foo"
    CMD ["/bin/echo", "foo"]
    ```

    - 하나의 Dockerfile에서 하나의 `CMD` 명령만 유효하고, 여러개가 있다면 마지막 것만 실행된다
- `ENTRYPOINT`: 컨테이너를 구동할 때 실행할 명령
    - `CMD`와 사용법이 똑같고, 역할은 비슷하다
    - 사용자가 어떤 인수를 명령으로 넘기더라도 Dockerfile에 명시된 명령을 그대로 실행한다

        ```docker
        ENTRYPOINT ["top"]
        CMD ["-d", "5"]
        ```

        - 위와 같은 파일로 컨테아너를 돌릴 시 5초마다 `top`가 실행된다

        ```bash
        docker build -t top .

        docker container run -it top # 5초마다 top 갱신
        docker container run -it top -d 10 # 10초마다 top 갱신
        ```

        - `ENTRYPOINT`는 사용자가 인수를 넘기는 것과 상관없이 무조건 실행되고 `CMD`는 인수를 통해 덮어쓸 수 있다
- `ONBUILD`: 이미지 빌드가 완료된 후 실행하는 명령
    - `ONBUILD`가 작성된 파일을 빌드해서 생성된 이미지를 베이스로 자식 이미지를 생성할 때 `RUN`과 함께 사용 가능하다

        ```docker
        FROM ubuntu:18.04

        ONBUILD RUN ["apt-get", "upgrade"]
        ONBUILD RUN ["apt-get", "-y", "install", "vim"]
        ```

    - 위와 같이 하면 부모 이미지를 생성할 때는 아무일도 일어나지 않는다
- `HEALTHCHECK`: 컨테이너 작동상태 체크
    - 컨테이너 내부에 로그를 남길 수 있다
    - 이 명령이 잘 동작하는지는 `docker ps`를 통해 `STATUS` 항목에서 확인 가능하다 (구동시간 옆 healthy라는 문구 표출)
- `ENV`: 환경변수 설정
- `WORKDIR`: 작업 디렉토리 할당
- `USER`: 사용자 할당
- `LABEL`: 이미지 버전 정보 등 등록
- `EXPOSE`: 포트번호 설정
    - 단순 참조용 성격만 가지고 있어서 컨테이너를 구동시 `-p` 옵션을 설정해줘야 한다
- `ADD`: 파일 복사 (웹 url 가능)
- `COPY`: 파일 복사