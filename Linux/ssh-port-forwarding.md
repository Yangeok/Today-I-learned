# SSH 포트 포워딩

- SSH 포트포워딩 혹은 SSH 터널링이라고 부른다
- 전제조건으로 원격지의 `sshd_config`에서 설정이 다음과 같아야 한다
  - `AllowTcpForwarding Yes`
  - `GatewayPorts Yes`
- 로컬 포트포워딩
  - 원격지 포트 `143`으로 접근하고 싶지만 로컬과는 방화벽으로 막혀있는 경우 터널을 뚫을 수 있다
  - 로컬 포트 `2001`로 접근하면 원격지 포트 `143`으로 제공되는 서비스를 접근하게 된다는 뜻이다

        ```bash
        ssh -L 2001:localhost:143 user@remote
        ```

        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e72ada6b-2a49-4ad4-82db-bb4e1d14fec5/Untitled.png)

  - 심화 1
    - 로컬에서 ssh로 접근가능한 원격지A가 있고, 원격지A와 통신가능한 원격지B의 포트 `143`이 있을 때도 터널을 뚫을 수 있다

            ```bash
            ssh -L 2001:remoteB:143 user@remoteA
            ```

            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ba2b012c-3348-4d26-93f1-3c41298004c6/Untitled.png)

  - 심화 2
    - 심화 1과 같은 상황에서 로컬에서 원격지C로 포트 `2001`를 포워딩하기 위해서 다음과 같이 할 수 있다

            ```bash
            ssh -g -L 2001:remoteB:143 user@remoteA
            ```

            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ce3bcfbb-d513-4307-ba93-c90bd72aff1b/Untitled.png)

- 리모트 포트포워딩
  - 원격지에서 로컬 포트 `143`으로 접근하고 싶지만 로컬에는 외부 접근 가능 IP가 없다
  - 원격지는 외부 접근 가능 IP가 있는 경우 터널을 뚫어 접근이 가능하다

        ```bash
        ssh -R 2001:localhost:143 user@remote
        ```

        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/791f0da9-53a8-4607-b3dc-4bf761eb3bc5/Untitled.png)
