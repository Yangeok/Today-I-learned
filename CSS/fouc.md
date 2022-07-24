# FOUC(Flash of Unstyled Content)란

- 외부 css를 불러오기 전에 잠시 스타일이 적용되지 않은 웹페이지가 나타나는 현상을 말한다.
- 마크업이 화면에 그려지고 나서 스타일이나 스크립트를 실행하는 경우 화면이 깜빡거릴 수 있다
- 해결방법
  - `head` 엘리먼트 안에 css 링크나 import 구문 사용을 자제해야 한다
  - html이 위에서 아래로 파싱하는 특징을 이용해 fouc를 유발하는 블락을 숨겼다가 다시 표시한다

        ```html
        <html>
            <head>
                <style>
                    .js #fouc {
                    display: none
                    }
                </style> 
                <script>
                    (function(H){H.className=H.className.replace(/\bno-js\b/,'js')})(document.documentElement)
                </script>
            </head>
            <body>
                <div id="fouc"> ... </div> <!-- /#fouc --> 
                <script> document.getElementById("fouc").style.display="block"; </script>
            </body>
        </html>
        ```
