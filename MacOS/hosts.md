# hosts 파일 수정

- DNS보다 먼저 호스트명을 IP로 변경해주는 파일이다
- 특별한 이유로 호스트명으로 통신을 해야하는 경우 변경해서 사용할 수 있다
- `/private/etc/hosts` 혹은 `/etc/hosts` 에서 수정할 수 있다
- DNS 캐시를 갱신하기 위해 `dscacheutil -flushcache` 를 한다
