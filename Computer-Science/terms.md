# 용어 정리

- marshalling
  - 객체의 메모리를 저장하거나 전송을 위해 적당한 자료형으로 변경하는 것을 말한다.
  - 다른 컴퓨터나 프로그램 간에 데이터를 이동시킬 경우 사용한다.
- serialization
  - 객체의 상태를 저장하기 위해 객체를 byte stream으로 변환하는 것을 말한다.
- semaphore
  - 공유된 자원의 데이터를 여러 프로세스가 접근하는 것을 막는 것
  - singaling 매커니즘으로 현재 공유자원에 접근할 수 있는 쓰레드, 프로세스의 수를 나타내는 값을 두어 상호배제를 달성하는 기법이다.
  - 파일시스템상 파일의 형태로 존재한다.
  - 소유할 수 없다.
- mutex
  - 공유된 자원의 데이터를 여러 쓰레드가 접근하는 것을 막는 것
  - 임계구역을 가진 쓰레드들의 러닝타임이 겹치지 않게 각각 단독으로 실행하게 하는 기술을 말한다.
  - mutex 객체를 두 쓰레드가 동시에 사용할 수 없으며, 무조건 1개의 key만 가진다.
  - 한 쓰레드, 프로세스에 의해 소유할 수 있는 key를 기반으로 한 상호배제 기법이다.
  - 소유가 가능하다.
  - 프로세스 범위에 속하므로 특정 프로세스가 사라질 때 깨끗이 삭제된다.
  - async한 서버를 쓰고 있는 경우 특정 구간에서는 뮤텍스처럼 컨텍스트가 바뀌어도 접근을 한 곳에서만 시켜야 하는 경우가 있을 때는 아래처럼 사용할 수 있다.

    ```ts
    class Mutex {
      constructor() {
        this.lock = false
      }
      async acquire() {
        while (true) {
          if (this.lock === false) {
            break
          }
          await sleep(100) // custom sleep
        }
        this.lock = true
      }
      release() {
        this.lock = false
      }
    }

    const mutex = new Mutex()
    (async () => {
      await mutex.acquire()

      ...

      mutex.release()
    })()
    ```
