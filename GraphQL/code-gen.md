# 코드젠 방법

- code first
  - 데코레이터와 클래스를 사용해서 graphql 스키마와 상응하는 것을 만드는 방식이다. typescript만을 사용하기 위한 경우 알맞은 방식이다.
  - `autoSchemaFile` 프로퍼티를 사용해 생성될 스키마의 위치를 집어넣어준다.
    ```ts
    GraphQLModule.forRoot({
      autoSchemaFile: join(process.cwd(), 'src/schema.gql')
    })
    ```
  - 혹은 값이 변경될때마다 변경되는 메모리에 넣어줄 수도 있다.
    ```ts
    GraphQLModule.forRoot({
      autoSchemaFile: true
    })
    ```
- schema first
  - 다른 플랫폼을 같이 사용하는 경우 다리 역할을 하는 dsl이 필요한 경우 사용하기 좋은 방식이다.
  - `typePaths` 프로퍼티에서 `.graphql` 파일들을 모두 찾아 메모리에 묶어놓는다.
  - 스키마들을 몇 개의 파일들로 나누고 resovler 근처에 위치시키기 위해 사용한다.
    ```ts
    GraphQLModule.forRoot({
      typePaths: ['./**/*.graphql']
    })
    ```
  - `@nestjs/graphql` 패키지로 자동으로 sdl을 만들어주기 위해 `definitions` 프로퍼티를 사용해야 한다.
    ```ts
    GraphQLModule.forRoot({
      definitions: {
        path: join(process.cwd(), 'src/graphql.ts')
      }
    })
    ```