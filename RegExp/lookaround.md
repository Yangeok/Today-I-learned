# lookaround 문법

- lookaround 문법
    - `X(?=Y)`: Y 앞에 있는 X를 찾는다 (positive lookahead)
    - `X(?!Y)`: Y앞에 없는 X를 찾는다 (negative lookahead)
    - `(?<=Y)X`: Y 뒤에 있는 X를 찾는다 (positive lookbehind)
    - `(?<!Y)X`: Y 뒤에 없는 X를 찾는다 (negative lookbehind)
- 결과를 소모하지 않고 문자열을 붙이는 방법
    - 정규식으로 어떤 문자열을 찾고, 그 뒤에 문자열을 붙여야하는 경우 사용할 수 있다
    - lookahead는 다음과 같이 사용한다

    ```jsx
    let str = 'XXXYYY'

    // X 앞에 1 붙이기 (positive)
    str.replace(/(?=X)/g, '1') // 1X1X1XYYY

    // X 앞이 아닌 곳이 1 붙이기 (negative)
    str.replace(/(?!X)/g, '1') // XXX1Y1Y1Y1
    ```

    - lookbehind는 다음과 같이 사용한다

    ```jsx
    let str = 'XXXYYY'

    // X 뒤에 1 붙이기 (positive)
    str.replace(/(?<=X)/g, '1') // X1X1X1YYY

    // X 뒤가 아닌 곳이 1 붙이기 (negative)
    str.replace(/(?<!X)/g, '1') // 1XXXY1Y1Y1
    ```