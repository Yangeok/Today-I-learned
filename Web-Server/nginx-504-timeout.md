# nginx 504 timeout 에러 해결하기

- reverse proxy로 서버를 운영할때 대용량 파일을 업로드하거나 요청 응답이 지연될 때 504를 뱉는다. 아래와 같이 `location` 블락에 설정을 추가한다.

```sh
server {
 listen 80;
 server_name http://localhost;

 location / {
  proxy_pass http://localhost;
  proxy_content_timeout 300;
  proxy_send_timeout 300;
  proxy_read_timeout 300;
  send_timeout 300;
 }
}
```
