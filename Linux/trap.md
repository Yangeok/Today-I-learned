# trap 사용법

- 쉘스크립트에서 인터럽트 시그널 처리를 할 때 사용하는 명령어이다
- 시그널을 중간에 가로채서 시그널에 해당하는 행동을 하지 못하게 막을 수도 있다
- 스크립트를 제작한 후 이 스크립트가 실행되는 도중 cmd + c를 입력하지 않도록 하는 경우 사용한다
- 아래와 같이 쉘스크립트에서 cmd + c를 막는지 확인하기 위한 무한루프 스크립트를 짤 수 있다

```bash
#!/bin/bash

trap 'echo "Failed" SIGINT'

while true;
do
 ehco 'Infinite loop'
 sleep 1
done
```
