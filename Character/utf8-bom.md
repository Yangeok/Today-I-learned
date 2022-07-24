# utf8-bom

- utf8 bom 조건에 만족하기 위해 파일의 첫 라인에 바이트코드 `\xEF\xBB\xBF`를 삽입해야 했음
- `sed`
  - linux

        ```bash
        sed -i '1s/^/\xEF\xBB\xBF/' <file_name>
        ```

  - macos

        ```bash
        sed -i '' '1s/^/\xEF\xBB\xBF/' <file_name>
        ```

- `xxd`

    ```bash
    xxd <file_name> | head
    ```

  - `-g`: 값은 `n`으로 표시할 라인수
