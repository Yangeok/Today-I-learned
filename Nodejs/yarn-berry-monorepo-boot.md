# yarn berry 모노레포 부트스트랩

## 패키지 추가

- 프로젝트를 초기화합니다

```bash
cd <project_name>
yarn init -yp
```

- `package.json`를 다음과 같이 변경/추가합니다

```json
{
 "name": "yangeok",
 "workspaces": ["packages/*"]
}
```

- zero install(이하 pnp)을 사용하기 위해 `.yarnrc.yml` 파일은 다음과 같이 작성합니다. 사실 pnp는 `.yarnrc.yml` 파일이 필요 없습니다만, `node_modules` 설치로 변경을 쉽게 하기 위함입니다. `node_modules` 디렉토리에 패키지를 설치하기 위해서는 `nodeLinker`를 `node-modules`로 변경합니다

```yaml
nodeLinker: pnp # node-modules
```

## 플러그인 설치

- 소스코드에서 import 레퍼런스를 잘가져오기 위해 다음과 같이 vscode용 sdk를 설치합니다

```bash
yarn dlx @yarnpkg/sdks vscode
```

- 패키지의 `@types/*` 를 따로 설치하지 않아도 자동설치될 수 있도록 typescript 플러그인을 설치합니다. 그 외 필요한 플러그인도 함께 설치합니다

```bash
yarn plugin import typescript
```

## 서브레포(워크스페이스) 설치

- 서브레포를 `packages` 디렉토리 안에 만들고 초기화합니다

```bash
take packages/utils
yarn init -yp
```

- 서브레포의 `package.json`을 다음과 같이 변경합니다

```json
{
 "name": "utils"
}
```

- 루트 디렉토리의 `package.json`에 패키지(예를 들어 axios)를 설치하고, 서브레포 디렉토리의 `package.json`의 패키지에 심볼릭 링크를 걸어줍니다. 서브레포 디렉토리의 패키지를 설치합니다

```bash
# 루트 디렉토리
yarn add axios
yarn workspace @yangeok/utils add axios

# 서브레포 디렉토리
yarn
```

- 워크스페이스가 제대로 잡혔나 다음과 같이 확인할 수 있습니다
