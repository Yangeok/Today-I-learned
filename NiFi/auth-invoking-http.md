# 인증이 필요한 InvokeHTTP 사용법

- 전제조건
  - `GetFile`로 호출할 API url 리스트를 호출
  - 쪼개진 url을 `InvokeHTTP` 로 호출시 API 제공자가 주는 `accessToken`이 필요함
- 1트
  - `accessToken`은 별도의 플로우를 통해 받고, 파일로 저장하는 일련의 과정을 플로우로 짰다고 가정한다
  - url을 `InvokeHTTP`에서 호출하기 전에 url 리스트와 `accessToken`을 양쪽 upstream에서 호출한다
  - InvokeHTTP에 큐가 양쪽에서 쌓이게 된다
  - 순차적으로 큐를 덜어내는 과정에서 `accessToken`이 있는 큐 따로, url이 있는 큐 따로 처리를 한다
- 해결방법
  - `accessToken`을 파일로 저장해서 `GetFile`하는 플로우는 NiFi에서는 불가능하다
  - 별도의 인증이 필요하다면, 인증받은 키를 memcache DB에 따로 저장해서 호출해야 한다
  - cloudera에서는 memcache를 권장하지만, redis를 사용한다
  - redis를 로컬에 올려서 `PutDistributedMapCache` 프로세서로 연결한다
  - Cache Entry Identifier 속성에 저장하고자 하는 키로 저장한다
  - `redis-cli`에서 다음과 같이 확인할 수 있다

        ```
        > 127.0.0.1:6379> keys *
        1) "accessToken"
        
        > 127.0.0.1:6379> get accessToken
        1234
        ```

  - 정해진 주기대로 `accessToken`은 갱신되서 쌓이게 된다
  - `GetFile`을 사용해 `accessToken`을 가져올 자리에 `FetchDistributedMapCache` 프로세서를 사용해서 redis에 담아놨던 값을 뺀다
  - 플로우파일 변수에 `accessToken`을 추가하고, 프로세서를 시작한다
- 참조
  - [To get authentication token using InvokeHttps and use the token in subsequent RestApi call in ApacheNiFI](https://community.cloudera.com/t5/Support-Questions/To-get-authentication-token-using-InvokeHttps-and-use-the/td-p/314724)
  - [Implementing Invokehttp Processor In Nifi](https://community.cloudera.com/t5/Support-Questions/Implementing-Invokehttp-Processor-In-Nifi/td-p/319946)
