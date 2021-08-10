# 파싱 에러 발생시 대처방법

- 다음과 같은 에러가 발생하면 아래와 같이 해결할 수 있다

    > parsing error the keyword 'import' is reserved

- `@typescript-eslint/parser`를 설치한다

```bash
yarn add -D @typescript-esint/parser
```

- `.eslintrc` 파일에 `parser` 프로퍼티를 추가한다

```json
{
  "parser": "@typescript-eslint/parser"
}
```