# egrep 사용법

- and 검색: abc, xyz가 같은 라인에 있는 파일 검색

    ```bash
    grep 'abc' *.<filename> | grep 'xyz'
    ```

- or 검색: abc나 xyz 라인이 있는 파일 검색

    ```bash
    grep 'abc|xyz' *.<filename>
    ```

- nand 검색: abc는 포함됐지만, xyz가 없는 라인 검색

    ```bash
    egrep 'abc' *.<filename> | grep -v 'xyz'
    ```
