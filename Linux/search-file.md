# 원하는 문자열이 있는 파일 검색

- `grep` 사용

    ```bash
    grep -rIH '<검색할 문자열>' <대상파일 혹은 폴더> [--include '<*.특정 확장자>']
    ```

  - `-r`: 현재 폴더의 하위폴더까지 검색
  - `-H`: 파일명까지 함께 출력
  - `—Include`: 특정확장자만 검색

- `find` 사용

    ```bash
    find <대상파일 혹은 폴더> -type f -print | xargs grep -rin --color=auto '<검색할 문자열>' 2>/dev/null
    ```

  - find
    - `-type`: 찾은 파일이나 폴더 지정
    - `-print`: 검색결과 출력
  - grep
    - `-r`: 재귀 검색
    - `-i`: 중복 제거
    - `-n`: 라인 번호
