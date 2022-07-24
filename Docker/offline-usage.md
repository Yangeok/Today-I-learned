# 오프라인 환경에서 사용

## docker-compose

- 파일을 다른 곳으로 복사하기 위해 다음 디렉토리로 다운받습니다.

```bash
curl -L https://github.com/docker/compose/releases/download/1.14.0/docker-compose-`uname -s`-`uname -m` > ./docker-compose
```

- 다운로드한 바이너리에 실행 권한을 부여합니다

```bash
chmod +x ./docker-compose
```

- 원하는 곳으로 옮겨줍니다.

## docker 이미지

- 이미지를 파일로 다음과 같이 저장합니다.

```bash
docker save <image_name>/<version> > <file_name>.tar
```

- 이미지 파일을 다음과 같이 로드합니다.

```bash
docker load < <file_name>.tar # way 1
docker load -i <file_name>.tar # way 2
```
