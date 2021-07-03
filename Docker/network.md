# 네트워크 종류

- 기본 네트워크
    - 하나의 디폴트 네트워크에서 모든 컨테이너를 연결한다
    - `docker-compose.yml`을 실행하는 디렉토리 이름 뒤에 `_default`가 붙는다
    - 디폴트 네트워크 안에서 컨테이너간 통신 시에는 서비스 이름을 호스트명으로 사용할 수 있다
        - 아래와 같은 compose 파일이 있는 경우에 `docker-compose foo ping bar`를 하면 호스트명만으로 `ping`을 날려볼 수 있다

        ```yaml
        services:
        	foo:
        		image: foo
        		depends_on: 
        			- bar
        		ports:
        			- 8081:8080
        	
        	bar:
        		image: bar
        		ports:
        			- 3001:3000
        ```

    - 클라이언트 위치가 내부에 있는지 외부에 있는지에 따라 호출가능한 포트가 달라진다
        - 디폴트 네트워크 내부에서 `foo` 서비스에 접속할 때는 `8080` 포트로 접속이 가능하다
        - 디폴트 네트워크 외부에서 `foo` 서비스에 접속할 때는 `8081` 포트로 접속이 가능하다
- 커스텀 네트워크
    - 커스텀 네트워크를 추가하기 위해서는 compose 파일에 `networks` 블락을 서비스 내외부에 추가한다

        ```yaml
        services:
        	foo:
        		image: foo
        		depends_on: 
        			- bar
        		ports:
        			- 8081:8080
        		networks:
        			- default
        			- baz_net
        	
        	bar:
        		image: bar
        		ports:
        			- 3001:3000
        		networks:
        			- default
        			- baz_net

        networks:
        	baz_net:
        		driver: bridge
        ```

    - `docker network ls`를 치면 커스텀 네트워크가 추가된 것을 확인할 수 있다
- 외부 네트워크
    - 다른 compose 파일에서 선언한 네트워크(`ext_net`)에 접속하기 위해서는 아래와 같은 구문을 추가한다

        ```yaml
        networks:
        	default:
        		external:
        			name: ext_net
        ```

    - 또한 외부에서 생성된 네트워크이므로 앱을 `down` 시킬 때 해당 네트워크가 사라지지 않는다