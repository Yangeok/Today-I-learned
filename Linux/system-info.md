# 시스템 정보 확인

- cpu 정보 확인
    - `cat /proc/cpuinfo`: CPU 정보 자세히 보기
    - `lscpu`: CPU 정보 간단히 보기
    - `grep -c processor /proc/cpuinfo`: 가상코어 갯수
    - `grep ^processor /proc/cpuinfo | wc -l`: 물리코어 갯수
    - `grep 'cpu cores' /proc/cpuinfo | tail -1`: CPU당 물리코어 갯수
    - `cat /proc/cpuinfo | egrep 'siblings|cpu cores' | head -2`: 하이퍼쓰레딩 사용 여부. `siblings`의 값이 `cpu cores`의 2배라면 활성화가 된 경우다
- 커널 정보 확인
    - `uname -a`
- 메모리 정보 확인
    - `free -h`
- 디스크 정보 확인
    - `df -h`