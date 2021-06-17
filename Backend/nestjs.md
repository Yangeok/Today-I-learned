# Nestjs 소개

- module
  - 비슷한 기능을 하는 코드들을 모아서 모듈로 캡슐화한다. 일반적으로 crud에 대한 로직이 있는 service와 api를 제공하는 controller가 하나의 모듈이 될 수 있다.
  - 하나의 모듈은 다른 모듈의 기능이 필요할 때 import해서 다른 모듈의 기능을 이용할 수 있다. 
  - 비슷한 기능들을 하나의 모듈로 모으면 응집력을 높일 수 있다.
- 인스턴스 생성을 nest에 맡겨서 느슨한 결합을 할 수 있어 확장가능한 아키텍처 설계가 가능하다.
- controller
  - 해당 모듈을 호출할 수 있는 경로를 정의한다.
  - rest 방식으로 api를 정의하고 응답을 반환한다.
- provider
	- `Injectable` 데코레이터가 달려있고, 다른 모듈에 주입가능하다는 뜻이다.
- pipe: validation을 위해 사용할 수 있는 기능
- guard: authorization을 위해 사용할 수 있는 기능