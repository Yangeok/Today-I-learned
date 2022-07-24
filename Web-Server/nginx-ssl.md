# Nginx SSL 사용하기

- 원하는 가상호스트 구문을 아래와 같이 변경한다

```bash
# as-is
server {
 listen 80;
 server_name yangeok.xyz;
}

# to-be
server {
 listen 80;
 server_name yangeok.xyz;
 
 return 301 https://$host$request_uri;
}

server {
 listen 443 ssl;
 server_name yangeok.xyz;

 ssl_certificate /etc/nginx/ssh/ssl.crt;
 ssl_certificate_key /etc/nginx/ssh/ssl.key;

 location / {
  proxy_http_version 1.1;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_set_header X-Forwarded-Protocol $scheme;
    proxy_set_header X-Real_IP $remote_addr;
 }
}
```
