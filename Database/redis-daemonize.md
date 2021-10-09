# Redis 데몬 실행

- `epel`을 설치한 후 `redis`를 설치한다

```bash
yum install -y epel-release
yum install -y redis
```

- 백그라운드에서 실행하기 위해 다음과 같이 설정한다

```bash
# way1
redis-server --daemonize yes

# way2
# /etc/redis.conf
daemonize yes # no

redis-server /etc/redis.conf
```

- 프로세스 시작여부를 확인한다

```bash
ps aux | grep redis-server
```

- cli를 실행해본다

```bash
redis-cli
```
