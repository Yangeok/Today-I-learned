# Let's Encrypt SSL 인증서 발급 방법

- webroot
  - 특징
    - 사이트 디렉토리 내에 인증서 유효성을 확인할 수 있는 파일을 업로드해서 인증서를 발급하는 방법이다
    - 실제 동작하는 서버의 특정 디렉토리에 특정 파일 쓰기 작업을 통해 인증한다
    - 이 방식의 장점은 nginx를 중단시킬 필요가 없다
    - 단점은 인증 명령 하나에 하나의 도메인 인증서만 발급 가능하다
  - 방법
    - well-known이 있는 폴더를 지정한다

            ```bash
            mkdir -p /var/www/letsencrypt/.well-known/acme-challenge
            ```

    - 특정 폴더에 `letsencrypt.conf`를 만든다
    - nginx 설정파일에서 호출해온다

            ```bash
            # /etc/nginx/snippets/letsencrypt.conf
            location ^~/.well-known/acme-challenge/ {
             default_type 'text/plain';
             root /var/www/letsencrypt;
            }
            
            # /etc/nginx/nginx.conf
            include /etc/nginx/snippets/letsencrypt.conf;
            ```

    - 서버 블락에 ssl을 추가해준다

            ```bash
            server {
             listen 80 default_server;
             server_name example.com;
            
             include /etc/ngin/ssl/letsencrypt.conf;
            
             location / {
              return 301 https://$request_uri;
              expires epoch; # 301 리디렉션이 캐시되지 않기 위해 사용
             }
            }
            ```

    - 다음과 같이 ssl을 받기 위해 커맨드를 날린다

            ```bash
            certbot certonly --webroot --webroot-path=/var/www/letsencrypt -d example.com
            ```

- 웹서버
  - 특징
    - 웹서버에서 직접 ssl 인증을 실시하고 웹서버에 맞는 ssl 세팅값을 부여한다
    - 발급이나 갱신을 위해 웹서버를 중단시킬 필요가 없다
    - 인증서 갱신시 상황에 맞게 세팅을 자동으로 업데이트한다
    - 사용자가 세팅을 변경할 수는 있지만, 자동 업데이트시 반영되지는 않는다
  - 발급
    - 다음과 같이 ssl을 받기 위해 커맨드를 날린다

            ```bash
            # using nginx
            certbot --nginx -d example.com
            
            # using apache
            certbot --apache -d example.com
            ```

    - 자동으로 ssl 옵션을 적용해서 `/etc/letsencrypt` 폴더에 인증서를 받아준다
    - 커스텀 옵션을 사용할 수도 있지만, 옵션을 커스텀하면 매번 수작업으로 업데이트해줘야 한다
    - 인증서 자동갱신은 다음과 같이 할 수 있다

            ```bash
            certbot renew --dry-run
            ```

- standalone
  - 특징
    - 사이트 동작을 멈추고 이 사이트의 네트워크를 이용해 사이트 유효성을 확인하고 인증서를 발급하는 방식이다
    - 80번 포트로 가상 standalone 웹서버를 띄워 인증서를 발급받는다
    - 이 방식은 동시에 여러 도메인을 발급할 수 있다
    - 인증서 발급전 웹서버를 중단하고, 발급 완료 후 다시 웹서버를 구동해야하는 불편함이 있다
  - 발급
    - 인증서를 받는동안 웹서버를 내린다
    - 인증서를 받기 위해 다음과 같은 커맨드를 날린다

            ```bash
            certbot certonly --standalone -d example.com
            ```

    - 인증서를 여러개 받기 위해서 다음과 같은 커맨드를 날린다

            ```bash
            certbot certonly --standalone -d example.com -d example1.com
            ```

    - 하지만 나중에 사이트를 없앨 때 불편할 수도 있다
    - 위의 경우 example.com 이름을 딴 폴더 아래 나머지 개수만큼 `.pem` 파일이 만들어진다
    - 귀찮더라도 사이트 별로 명령어를 따로따로 날려주는 것이 관리에는 더 용이하다
- dns
  - 특징
    - 도메인을 쿼리해 확인되는 txt 레코드로 사이트 유효성을 확인하는 방법이다
    - 와일드 카드 방식으로 인증서를 발급 가능하다
    - 서버 관리자가 도메인 dns를 관리/수정할 수 있어야 한다
    - 인증서 갱신시마다 dns에서 txt를 변경해야하므로 외부에서 txt 레코드를 입력할 수 있도록 dns가 api를 제공하는 경우만 갱신을 자동으로 처리하는 것이 가능하다
  - 방법
    - 클라우드플레어를 사용하는 경우 `.ini` 파일에 다음과 같이 api 토큰을 입력해준다

            ```bash
            dns_cloudflare_api_token = 'TOKEN'
            ```

    - 파일 권한을 `600`으로 변경한다
    - 클라우드플레어 dns 인증 플러그인 `certbot-dns-cloudflare`을 서리한다
    - 인증서를 발급받기 위해 다음과 같은 커맨드를 날린다

            ```bash
            certbot certonly --dns-cloudflare --dns-cloudflare-credentials ./cloudflare.ini -d *.example.com --preferred-challenges dns-01
            ```

    - 인증서를 다음과 같이 post hook을 이용해서 자동갱신할 수 있다

            ```bash
            30 4 * * 0 certbot renew --quite --post-hook "nginx reload" > /dev/null 2>&1
            ```
