## 렌더링 타입별 추적방법

- csr
  - 클라이언트측 이동경로 확인은 pageview api를 사용하면 추적할 수 있다. `page_title`, `page_location`, `page_path`	총 3개의 프로퍼티를 가진 api이다.
  - `gtag.js`를 가져와서 다음과 같이 spa에서 세팅할 수 있다. 페이지 제목은 `document.title`에서, 전체경로는 `location.href`에서, 경로는 `location.pathname`에서 찾을 수 있다.
    ```ts
    gtag('config', 'UA-XXXXXXXX-X', {
      page_title: 'title',
      page_location: 'http://example.com/path/to/title',
      page_path: '/path/to/title'
    })
    ```
- ssr
  - nextjs를 사용하는 경우는 아래와 같이 document 파일에서 가장 먼저 동작할 스크립트인 `addGAScript` 메서드를 작성해준다.
  - 각 페이지에 모두 포함되는 컴포넌트에 `addGaScript`에 인자로 주입될 url을 인자로 갖는 함수 `handleRouteChangeComplete`와 이벤트 리스너를 붙여준다.