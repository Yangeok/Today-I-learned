# xargs 사용법

- `find`, `ls`, `cat` 등 뒤에 파이프로 추가해서 사용한다
- 30일 이상 된 파일명 뒤에 .bak 추가

    ```jsx
    find . -mtime +30 | xargs mv -i {} {}.bak
    ```

- `find`한 파일 제거

    ```jsx
    find . -name *.mp3 | xargs rm
    ```

- 가져온 목록에 각각 파일 내용을 cat으로 읽고 병합 파일 생성

    ```jsx
    ls *.txt | xargs cat >> abc.merge
    ```
