## scp usage

- 단일 파일을 로컬 → 원격으로 보낼 때

```bash
$ scp /path/to/filename USER@HOSTNAME:/path/to/filename
```

- 복수 파일을 로컬 → 원격으로 보낼 때

```bash
$ scp /path/to/filename1 /path/to/filename2 USER@HOSTNAME:/path/to/location
```

- 여러 파일을 포함한 디렉토리를 로컬 → 원격으로 보낼 때

```bash
$ scp -r /path/to/location USER@HOSTNAME:/path/to/location
```

- 단일 파일을 원격 → 로컬로 가져올 때

```bash
$ scp USER@HOSTNAME:/path/to/filename /path/to/filename
```

- 복수 파일을 원격 → 로컬로 가져올 때

```bash
$ scp USER@HOSTNAME:"/path/to/filename1 /path/to/filename2" /path/to/location
```

- 여러 파일을 포함한 디렉토리를 원격 → 로컬로 가져올 때

```bash
$ scp -r USER@HOSTNAME:/path/to/location /path/to/location
```

- 옵션
    - `—r`: 디렉토리 내 모든 파일/디렉토리
    - `—p`: 원본 권한 속성 유지 복사
    - `—P`: 포트 번호 지정 복사
    - `—c`: 압축 복사
    - `—v`: 과정 출력 복사
    - `—a`: 아카이브 모드 복사