# openssl 사용법

- 브라우저와 서버간 통신을 암호화하는 오픈소스 라이브러리이며, 웹서버에서 자유롭게 사용할 수 있다
- Tableau Server에 SSL을 사용하려는 경우는 Root 인증서까지도 생성해야하기 때문에 Root 인증서에도 서명이 필요하다. 이 경우를 SSC(Self Signed Certificate)라고 부른다
- 아래와 같이 개인키와 인증서 서명 요청 파일을 만든다

    ```bash
    openssl req -new -newkey rsa:2048 -nodes -keyout test.csr
    ```

- SSL 인증서를 생성한다

    ```bash
    openssl x509 -req -days 365 -in test.csr -signkey test.key -out test.crt
    ```

- 다음과 같은 파일들을 확인할 수 있다
  - `test.key`: 암호키 파일
  - `test.csr`: 인증 요청 파일
  - `test.crt`: 인증서 파일
