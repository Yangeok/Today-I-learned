# Deep learning algorithms

- msa용 mono-repo 작성하는데 유용한 유틸리티 라이브러리이다.
- 단일저장소에서 다양한 패키지를 구성할 수 있다.
- 모든 프로젝트마다 공통적으로 eslint, prettier, babel 등을 루트에서 한 번만 설정해서 링크하는 것이 가능해진다.
- 패키지를 넘나들어 코드를 재사용하는 것이 가능해진다.
- 명령어셋
  - `init`: 해당 프로젝트에 lerna repo를 만들거나 최선버전으로 업데이트할 때 사용한다.
  - `version`: semver 키워드를 입력해서 명시하도록 도와준다.
  - `diff [package]`: 해당 패키지의 지난 배포 이후 변경점을 보여준다.
  - `bootstrap`: 각 패키지의 의존을 설치하고 재정비해준다. 의존이 있는 패키지는 symbolic link로 연결한다.
  - `run`: 각 패키지의 npm 명령어를 실행한다. 스코프를 지정할 수도 있다.
  - `publish`: 지난 릴리즈 이후에 변경이 있었던 패키지를 배포한다.
  - `clean`: 각 패키지의 `node_modules`를 삭제한다.
  - `link convert`: `devDependencies`를 루트에서 관리할 수 있다.
- 릴리즈를 분리해서 하는 것이 가능하다.