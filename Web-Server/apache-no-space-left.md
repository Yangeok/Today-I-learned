# Apache 에러 No space left on device

- 아파치를 재시작하려고 하면 프로세스를 생성하지 못하고 아래와 같은 에러를 리턴하는 경우가 있다

    > No space left on device: AH00023: Couldn't create the rewrite-map mutex

- 프로세스간 데이터 공유를 위해 세마포어를 생성한다. 아파치가 비정상적으로 종료되는 경우 생성된 세마포어가 삭제되지 않고 큐에 계속 쌓이면 위와 같은 문제가 생긴다
- `ipc -s` 명령어로 `semid`와 연결된 `pid`가 있는지 확인해볼 수 있다
- 다음과 같은 쉘스크립트 파일을 만들어 세마포어를 삭제하면 에러가 사라지는 것을 확인할 수 있다

```bash
#!/bin/bash
## Semaphore Arrays - pid 검사를 통해 종료된 pid 값을 가진 Semaphore Arrays를 종료 시킨다. 
for a in `/usr/bin/ipcs -s|awk '$2~/[0-9]/{print $2}'`
  do sem_pid=`ipcs -si $a|sed '/^$/d'|tail -1|awk '$5~/[0-9]/{print $5}'`
  if [[ -z  `ps -e|awk '$1~/^'$sem_pid'$/{print}'` ]];then /usr/bin/ipcrm -s $a;fi
  done
```

- 세마포어, 뮤텍스는 병렬작업을 하는데 필수로 사용되며 무한생성은 불가능하다.
- 다음과 같은 명령어로 시스템의 제한 수치를 확인할 수 있다

```bash
ipcs -ls
```
