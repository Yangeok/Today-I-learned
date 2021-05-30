# 지연된 Promise

- with `reduce()`
  - 비동기 코드를 처리할 때 Promise를 사용하면 편하다.
  - 하지만 ajax를 통해 순차적인 처리를 할 때, 시간을 두고 하나씩 처리할 때 아래와 같은 방법을 활용할 수 있다.
    ```ts
    let arr = [1, 2, 3, 4, 5]

    // using thenable syntax
    arr.reduce((prevPromise, nextId) => {
      return prevPromise.then(() => methodThatReturnsAPromise(nextId))
    }, Promise.resolve())

    // suing async/await syntax
    arr.reduce(async (prevPromise, nextId) => {
      await prevPromise
      return methodThatReturnsAPromise(nextId)
    }, Promise.resolve())
    ```
- delay
  - api 콜 후에 딜레이를 추가하고 싶은 경우 아래와 같이 할 수 있다.
    ```ts
    const delayPromise = <T>(val: T, ms: number) => {
      return Promise<T>(resolve => setTimeout(resolve, ms, val))
    }

    // example usage
    const [data] = await Promise.all([
      delayPromise(await axios.get('foo'), 1000)
    ])
    ```