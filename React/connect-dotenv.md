# dotenv 변수 연결해서 사용하는 방법

- [dotenv-cli](https://www.npmjs.com/package/dotenv-cli)
  - 예시

    ```jsx
    "scripts": {
        "start": "react-app-rewired start",
        "build-dev": "dotenv -e .env.development react-app-rewired build",
        "build-prod": "dotenv -e .env.production react-app-rewired build",
        "build": "react-app-rewired build",
        "test": "react-app-rewired test --env=jsdom",
        "eject": "react-scripts eject"   
    }
    ```

- dotenv
  - 예시
