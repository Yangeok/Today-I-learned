# Nginx https 설정시 ERR_TOO_MANY_REDIRECTS 에러 대처방법

- cloudflare에 도메인을 등록하고, openssl로 nginx에 커스텀 SSL 인증서를 아래와 같은 옵션으로 사용하는 경우 `ERR_TOO_MANY_REDIRECTS`를 만날 수도 있다

```bash
server {
       listen          80;
       server_name     yangeok.xyz;

       return 301 https://$host$request_uri;
}

server {
        listen          443 ssl;
        server_name     yangeok.xyz;

        ssl_certificate /home/ubuntu/.ssh/ssl2/test.crt;
        ssl_certificate_key /home/ubuntu/.ssh/ssl2/test.key;

        location / {
                proxy_http_version 1.1;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header Host $http_host;
                proxy_set_header X-Forwarded-Protocol $scheme;
                proxy_set_header X-Real_IP $remote_addr;
        }
}
```

- 이 경우 cloudflare에서는 아래와 같이 알려주고 있다

    > 원본 웹 서버 구성에서 HTTPS에서 HTTP로의 리디렉션 또는 HTTP에서 HTTPS로의 리디렉션을 제거하세요.

    > SSL/TLS 앱 개요 탭에서 Cloudflare SSL 옵션을 업데이트하세요.

- 2가지 방법이 있다고 한다
    - nginx http 블락에서 https로 리디렉션 시키는 블락을 삭제시킨다

    ```bash
    # server {
    #        listen          80;
    #        server_name     yangeok.xyz;
    # 
    #        return 301 https://$host$request_uri;
    # }
    ```

    - SSL/TLS 탭에서 SSL 옵션이 ***유연***으로 설정된 경우 ***전체***로 변경한다