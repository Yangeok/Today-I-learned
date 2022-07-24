# datetime 시리얼라이징 에러 해결방법

- dict를 json으로 저장하려고 하면 다음과 같은 에러가 발생하는 경우가 있다

    > TypeError: datetime.datetime(2012, 8, 8, 21, 46, 24, 862000) is not JSON serializable

- json으로 저장할때 `dumps()`의 옵션을 지정하면 문자열 자체로 저장시킬 수 있다

    ```docker
    json.dumps(dict, default=str)
    ```
