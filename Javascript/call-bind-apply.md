# bind, call, apply

- bind
  - 함수나 메서드에 bind를 사용하면 인자로 들어간 값이 this가 된다

  ```js
  function sum(num) {
    return num + this.num1  + this.num2
  }

  const foo = sum.bind({ num1: 10, num2: 5 })

  console.log(foo(5)) // 20
  ```

- call
  - 함수나 메서드를 다음과 같이 실행한다
  - 인자를 하나씩 넘긴다

  ```js
  function info(a, b) {
    return a + b + this.x + this.y
  }

  info.call({ x: 10, y: 20 }, 30, 40)
  ```

- apply
  - 함수나 메서드를 다음과 같이 실행한다
  - 인자를 배열로 넘긴다

  ```js
  function info(a, b) {
    return a + b + this.x + this.y
  }

  info.apply({ x: 10, y: 20 }, [30, 40])
  ```
