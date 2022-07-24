# 용어 정리

- decorator: `.d.ts` 파일이나 declare class 안에는 사용할 수 없다. 데코레이터 표현식은 런타임에 함수로 호출된다.
- generic
  - 함수에서 사용

  ```ts
  // using primative type
  function foo(arg: any): any {
    return arg
  }

  // using generic
  function foo<T>(arg: T): T {
    return arg
  }

  // equals using arrow function
  const foo = <T>(arg: T): T => { // unclosed `T` tag error
    return arg
  } 

  // use `extends` on the generic
  const foo = <T extends unknown>(arg: T): T => {
    return arg
  }
  ```
