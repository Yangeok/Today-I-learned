# pgadmin에서 pgsql 인스턴스 호스트 찾기

- pgadmin에 postgresql을 docker로 구동할 때 `localhost`나 `127.0.0.1`을 찾지 못하는 경우 컨테이너 id를 다음과 같이 입력한다

```jsx
docker inspect CONTAINER_ID
```

- json으로 나오는 결과에서 `data[0].NetworkSettings.Networks.pgadmin_default.Gateway` 로 나오는 값을 [localhost](http://localhost) 대신 넣는다