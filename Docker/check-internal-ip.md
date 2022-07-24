# 인스턴스 내부 IP 확인

- 지금 돌고 있는 컨테이너를 확인한다

```sql
docker ps
```

- 아래와 같이 inspect를 찍어본다

```sql
docker inspect <instance_id_or_name> --format='{{range .NetworkSettings.Networks}}{{.Gateway}}{{end}}'
```
