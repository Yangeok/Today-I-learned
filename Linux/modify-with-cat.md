# 에디터 없이 cat으로 파일 수정

- `echo` 사용법

    ```bash
    # 덮어쓰기
    ehco "content" > file

    # 이어쓰기
    ehco "content" >> file
    ```

- `cat` 사용법

    ```bash
    # 덮어쓰기
    cat > file
    ...
    ^D # cmd + d

    # 덮어쓰기
    cat >> file
    ...
    ^D # 종료 cmd + d
    ```

- `<<EOF` 사용법

    ```bash
    cat <<EOF > file
    ...
    EOF # 종료
    ```