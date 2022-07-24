# readlink 사용법

- `readlink`는 심볼릭 링크의 정보를 읽고 출력하는 프로그램이다
- `-f` 옵션을 사용하면 심볼릭 링크 원본의 절대경로를 확인할 수 있다
- MacOS에서 `illegal option`이라고 나오는 경우는 `coreutils`에 들어있는 `greadlink`로 `readlink`를 대체하면 해결 가능하다
