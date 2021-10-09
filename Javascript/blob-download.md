# blob 파일 다운로드 구현

- 브라우저 javascript에서 api를 fetch하고 다운받기 위해 아래와 같은 시도를 했다
- 1트
  - `onClick` 이벤트 핸들러 안에 fetch 후 다음과 같은 코드를 사용했다

    ```jsx
    const data = await(await fetch(url)).blob()
    
    window.location.assign(window.URL.createObjectURL(data))
    ```

  - 다운로드 파일명을 지정했음에도 uuid 형식의 파일명으로 다운로드가 됐다
- 2트
  - a 태그를 하나 만들어 다운로드 시에만 사용하고 바로 엘리먼트를 제거한다

    ```jsx
    const url = window.URL.createObjectURL(blob)
    
    const a = document.createElement('a')
    a.href = url
    a.download = `${i.table}.csv`
    a.click()
    a.remove()
    
    window.URL.revokeObjectURL(url)
    ```

  - 원하는 파일명으로 파일을 다운받을 수 있다
- `URL.createObjectURL()`
  - 인자로 들어가는 객체를 가리키는 url을 dom 문자열로 반환한다
  - 생성한 blob url은 `documnet`에서만 유효하기 때문에 다른 브라우저에서는 사용할 수 없다
- `URL.revokeObjectURL()`
  - `createObjectURL`로 생성한 url을 더 이상 사용하지 않을 때, 브라우저 메모리에서 해제하기 위해 사용하는 메서드이다
  - 이 메서드를 통해 url을 해제하지 않으면 gc가 동작하지 않아 잠재적으로 메모리 누수를 안고 갈 수 있다
