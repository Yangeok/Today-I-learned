# 네트워크

- 호스트-컨테이너간 네트워크

    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d719de88-6753-4c8c-9741-2c939dca5ca1/Untitled.png)

  - NIC(Network Interface Controller)
    - 랜카드라고 부르는 컨트롤로러 물리적으로 구성된 NIC는 `ens33`으로 인식된다
    - `eth0` 또한 물리 NIC이다
  - NAPT(Network Address Port Translation)
    - IP와 포트를 변환하는 기술이다
    - 도커 엔진이 컨테이너에 부여한 IP는 사설 IP로 호스트에서 직접 접근이 불가능하기때문에 변환이 필요했다
    - 호스트의 각 포트에 컨테이너 IP와 포트를 매핑시켜주는 역할을 한다
  - docker0
    - 브릿지 형태의 네트워크이며 도커 엔진을 실행하면 자동으로 생성된다
    - 컨테이너를 실행하면 내부의 모든 포트를 `docker0`이라는 가상 브릿지에 개방한다
    - 호스트는 NIC에 직접 컨테이너와 연결하지 않고, 브릿지를 경유한다
    - 포트를 통해 각 컨테이너에 접근할 수 있는 다리를 놓아주는 역할을 한다
  - vethOOO
    - 컨테이너를 띄우고 호스트에서 `ifconfig`를 치면 v`e`th로 시작하는 NIC가 보이는데, 컨테이너와 통신하기 위한 가상 NIC이다
    - `veth` + 난수 형태로 만들어진다
    - `eth0`이라고 표시된 이유는 호스트 입장이 아닌 컨테이너 입장에서 가상 NIC를 `eth0`으로 인식하기 때문이다
- 컨테이너-컨테이너간 네트워크
  - bridge

        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ecff0232-2cb9-4ebe-ac29-d1a0397122e2/Untitled.png)

    - `docker0`을 게트웨이로 해서 컨테이너가 생성된 순서대로 IP가 부여된다
    - 컨테이너 구동시 별도의 네트워크 설정을 하지 않으면 모두 `docker0` 브릿지 네트워크에 연결된다
    - 같은 대역의 네트워크에서 컨테이너가 구성됐기때문에 통신이 서로 가능하다
    - 커스텀한 별도의 브릿지 네트워크를 구축해서 컨테이너를 구성한다면 기존 `docker0`에 구성된 컨테이너와는 통신이 불가능하다
  - host

        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a10a0e8a-b4de-43b2-8884-fb8d47b48fa4/Untitled.png)

    - 도커 엔진이 작동하고 있는 호스트의 IP를 그대로 사용한다
    - 브릿지를 통해 NAPT 과정을 거치지 않아도 되며, 컨테이너의 포트를 명령어에 작성하지 않아도 된다
    - 리눅스에서만 지원된다
  - none
    - 컨테이너를 격리된 공간에 차단시켜놓고 어떠한 네트워크와도 연결하지 못하게 하는 것을 가리킨다
- 네트워크 명령어
  - `ls`: 네트워크 목록 조회
    - `—filter`: 특정 조건에 필터를 걸 수 있다
  - `create`: 네트워크 생성
    - `—driver`: 네트워크 타입을 지정할 수 있다 (기본값 `bridge`)
  - `connect`: 컨테이너를 네트워크에 연결
    - 기본 브릿지 네트워크는 유지하면서 새로운 브릿지와 연결시킬 수 있다
    - 하나의 컨테이너가 두개의 네트워크에서 공유될 수 있다
    - 단, 2개의 네트워크는 게이트웨이가 각각 다르다
  - `disconnect`: 컨테이너를 네트워크에서 해제
  - `inspect`: 네트워크 상세정보 조회
  - `rm`: 네트워크 삭제
