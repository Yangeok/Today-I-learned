# 용어 정리

- class
  - constructor는 인스턴스를 생성하고 초기화하는 역할을 수행한다. `new Foo()`를 실행하면 `Foo.prototype.constructor`가 호출된다. constructor는 필수는 아니지만 부모의 메서드를 호출하고싶은 경우에는 `constructor`를 작성해줘야 한다.
- `Reflect`
  - 중간에 가로챌 수 있는 메서드를 제공하는 내장객체이다.
  - 메서드 종류가 proxy handler와 동일하다.
  - 함수 객체가 아니므로 생성자로 사용할 수 없다.
