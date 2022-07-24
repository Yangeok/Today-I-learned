# URL vs. URLSearchParams

- `URL`
  - `hash`: `#`와 문자열을 담고 있음
  - `host`: 도메인(=호스트명)과 포트를 담고 있음
  - `hostname`: 도메인
  - `href`: 전체 URL을 반환하는 문자열
  - `origin`: URL의 출처인 스킴을 담고 있음
  - `password`: 도메인 이름 이전에 지정된 비밀번호를 담고 있음
  - `pathname`: `/`와 경로를 담은 문자열
  - `port`: 포트
  - `protocol`: 프로토콜 스킴과 `:`을 포함
  - `search`: `?`로 시작되는 매개변수를 나타내는 문자열
  - `searchParams`: `URLSearchParams` 객체
  - `username`: 도메인 이름 이전에 지정된 사용자명을 담고 있음
- `URLSearchParams`
  - `append()`: 파라미터를 추가하는 메서드
  - `toString()`: 문자열로 파라미터를 치환하는 메서드
