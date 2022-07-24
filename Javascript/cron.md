# 함수 스케쥴링 돌리기

- `cron`을 사용해서 아래와 같은 래퍼함수를 써야 함

    ```jsx
    import { CronJob } from 'cron'

    function runSomething() {

    }

    function startScheduledJob() {
     return new CronJob('* * * * *', runSomething).start()
    }
    ```
