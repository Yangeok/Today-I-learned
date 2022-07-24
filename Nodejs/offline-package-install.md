# 오프라인 환경에서 패키지 설치

## 온라인 서버

- 오프라인에서 `yarn berry`를 설치하는 것이 불가능하기때문에 사용자 루트 디렉토리에서 v1으로 변경한다

```bash
cd ~

yarn set version classic # to v1
# yarn set version berry # to v3
```

- 프로젝트 디렉토리에서 `.yarnrc` 파일을 만든다

```bash
yarn-offline-mirror './npm-packages-offline'
yarn-offline-mirror-pruning true
```

- 캐시를 날리고, `npm-packages-offline` 디렉토리로 `.zip` 파일을 만들기 위해 패키지 다운로드를 한다

```bash
yarn cache clean
yarn
```

## 오프라인 서버

- 압축된 패키지들을 설치한다
