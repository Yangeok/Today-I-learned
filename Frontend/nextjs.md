# Nextjs 소개

- `withHead`: 페이지마다 각각 페이지에 맞는 head를 적용할 수 있는 hoc 함수

    ```ts
    // component/hocs/withHead.tsx
    import Head from 'next/head'

    const withHead = (Component, title, description) => {
      const Comp = props => (
        <>
          <Head>
            <title>{title}</title>
            <meta name="description" content={description} />
          </Head>
          <Component {...props} />
        </>
      )

      return Comp
    }
    
    export default withHead

    // pages/foo.tsx
    const Foo = props => {
      (...)
    }
    
    export defalt withHead(Foo, 'Foo', 'This is Foo page')
    ```

- `app.js`, `_document.js`에서는 `window` 객체를 사용할 수 없다.
- 최초로 실행되는 것은 `app.js`이다. props로 들어있는 `pageProps`는 페이지마다 있는 메서드인 `getInitialProps`를 통해 내려받은 props이다.
- 그 다음 실행되는 것이 `document.js`이다. static html을 구성하기 위해 `app.js`에서 구성한 html이 어떤 식으로 들어갈지 구성하는 파일이다.
- `document.js`에는 애플리케이션 로직은 넣지 말아야한다.
- csr을 통해 데이터를 fetch하면 `useEffect`로 컴포넌트가 마운트되고 나서 한다.
- `getInitialProps`를 통해 데이터 fetch하는 과정을 빠르게 처리할 수 있다. v9.3부터는 `getStaticProps`, `getStaticPaths`, `getServierSideProps`를 사용한다.
- 데이터 fetch를 서버에서 하면 속도가 빨라지고, 코드를 분리할 수 있어 코드가 깔끔해진다.
데이터가 꼭 필요한 페이지의 경우 브라우저가 데이터를 가져올 때까지 화면 렌더링을 잠시 `null`로 처리하는 경우가 있는데, 이 경우를 없앨 수 있다.
- `getInitialProps` 내부로직은 서버에서 실행되므로, 클라이언트에서 수행가능한 로직은 피해야한다.
- 한 페이지를 로딩할때 하나의 `getInitialProps`만 실행된다. `app.js`에서 `getInitialProps`를 실행한 경우 그 하위 페이지에서는 실행되지 않는다.
  - `getStaticProps`: ssr 전용으로 빌드할 때 데이터를 가져온다. js 번들에 포함되지 않는다. pages 폴더에서만 사용이 가능하다. seo가 적용된 pre-render와 캐싱할 수 있다. cms에서 게시글 목록을 가져와야할 경우에 사용한다.

    ```ts
    import {GetStaticProps} from 'next'

    const getStaticProps: GetStaticProps = async ctx => {
      const {params, preview, previewData} = ctx

      const res = await fetch('https://example.com')
      const data = await res.json()

      return { props: { data }}
    }
    ```

  - `getStaticPaths`: ssr 전용으로 pre-render할 동적 경로를 지정한다. `getStatucProps`와 같이 쓰는데 렌더링할 경로 목록을 정의할 수 있다. 지정된 경로를 정적으로 pre-render할 수 있다. pages 폴더에서만 사용 가능하며 `getServerSideProps`와는 사용할 수 없다.

    ```ts
    import {GetStaticPaths} from 'next'
    const getStaticPaths: GetStaticPaths = asnyc () => {
      return { 
        paths: [{
          params: { id: 1 }
        }],
        fallback: true
      }
    }
    ```

    - `fallback`은 기본값이 false로 경로 지정페이지만 pre-render를 하고 없는 경로 접근시 404페이지를 렌더한다. true 설정시 fallback 페이지를 렌더링해 로딩페이지를 렌더링한 후 `getStaticProps`를 실행해 필요한 데이터를 가져온다.

      ```ts
      import {useRouter, GetStaticPaths, GetStaticProps} from 'next/router'
      const Comp = props => {
        const router = useRouter()
        if (router.isFallback) {
          return <div>Loading...</div>
        })
        return (
          <div>pre-render page</div>
        )
      }
      const getStaticPaths: GetStaticPaths = async () => {
        const res = await fetch('https://example.com')
        const data = await res.json()

        const paths = data.map(({ title }) => ({ params: { title}}))

        return { paths, fallback: false }
      }
      const getStaticProps: GetStaticProps = async ({ params }) => {
        const res = await fetch(`https://example.com/${params.title}`)
        const data = await res.json()

        return { props: { data }}
      }
      ```

  - `getServerSideProps`: ssr 전용으로 `getInitialProps`는 클라이언트, 서버 양 쪽 다 실행되지만 이 api는 서버에서만 실행된다. ctx 객체에는 params, req, res, query, preview, previewData가 포함된다.

    ```ts
    import {GetServierSideProps} from 'next'
    
    const getServerSideProps: GetServerSideProps = async () => {
      const res = await fetch('https://example.com')
      const data = await res.json()

      return { props: { data }}
    }
    ```
