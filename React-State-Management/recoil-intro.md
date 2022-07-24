# React 상태 관리 도구

- recoil
  - `useRecoilState(state): [state, setterOrUpdater]`
    - `state`는 `atom`이나 writable `selector`가 들어간다. writable `selector`는 `get`, `set` 프로퍼티를 모두 가지고 있는 `selector`를 말한다. read-only `selector`는 `get` 프로퍼티만 가지고 있다.
    - 인자에 기본값 대신 recoil state가 들어가는 점을 제외하고는 `React.useState`와 사용법이 비슷하다.
  - `useRecoilValue(state): state`
    - `state`는 `atom`이나 `selector`가 들어간다.
    - 컴포넌트에서 상태를 쓰기 작업 없이 읽기만 하려는 경우에 사용한다. read-only, writable에 상관없이 모두 사용가능하다.
    - `atom`은 writable이고, `selector`는 read-only나 writable 둘 중에 하나라는데 무슨 말인지 이해가 안된다!!
  - `useSetRecoilState(state): setterOrUpdater`
    - `state`는 writable한 상태가 들어간다.
    - 비동기적으로 상태를 바꾸기 위해 사용하는 setter 함수를 반환한다.
    - 인자에 이전값을 받는 setter는 새로운 값, updater 함수 모두 가능하다.
  - `useResetRecoilState(state)`
    - `state`는 writable한 상태가 들어간다.
    - 상태가 변경되면 언제나 일어나는 re-render를 구독하지 않고, 컴포넌트의 상태값을 기본값으로 돌려놓고 싶은 경우에 사용한다.

- recoil: atom에서 시작해 selector를 거쳐 react 컴포넌트까지 전달되는 하나의 data flow graph를 만든다.
  - atom
    - 상태의 단위로 업데이트되면 해당 atom을 구독하던 모든 컴포넌트들이 새로운 값으로 리렌더 된다.
    - 상태를 구독하는 컴포넌트들은 모두 상태를 동일하게 유지한다.

      ```ts
      const fontSizeState = atom({
        key: 'fontSizeState',
        default: 14
      })

      const FontButton = () => {
        const [fontSize, setFontSize] = useRecoilState(fonSizeState)

        const handleClick = useCallback(() => {
          setFontSize(size => size + 1)
        }, [setFontSize])

        return (
          <>
            <p>{fontSize}</p>
            <buton onClick={handleClick} />
          </>
        )
      }
      ```

    - id를 key에 동적으로 부여할 수도 있다.

      ```ts
      const itemWithId = id => atom({
        key: `item-${id}`,
        default: ''
      })

      const Layer = ({ id }) => {
        const [item, setItem] = useRecoilState(itemWithId(id))
      }
      ```

    - 비동기 모드도 지원한다. suspense를 사용하면 바로 사용 가능하다.

      ```ts
      const getUserProfile = async userId => {
        const data = await fetch('foo')
        return data.json()
      }

      const const userIdState = atom({
        key: 'userIdState',
        default: null
      })

      const userProfileState = selector({
        key: 'userProfileState',
        get: async ({ get }) => {
          const userId = get(userIdState)
          const data = await getUserProfile(userId)
          return data
        }
      })

      const Profile = () => {
        const userProfile = useRecoilValue(userProfileState)
      
        return (
          <div>{userProfile.name}</div>
        )
      }

      const ProfileRenderer = () => {
        return (
          <Suspense fallback={<LoadingIndicator />}>
            <Profile />
          </Suspense>
        )
      }
      ```

  - selector
    - 다른 atom이나 selctor를 받아 사용하는 순수함수이다.
    - 받은 atom이나 selctor들 중 어떤 것이 업데이트되면 selector함수는 재평가된다.
    - atom처럼 구독이 가능하고 selctor가 재평가될 때 컴포넌트가 리렌더된다.

      ```ts
      const fontSizeState = atom({
        key: 'fontSizeState',
        default: 14
      })

      const fontSzieLabelState = selector({
        key: 'fontSizeLabelState',
        get: ({ get }) => {
          const fontSize = get(fontSizeState)
          const unit = 'px'

          return `${fontSize}${unit}`
        }
      })

      const FontButton = () => {
        const setFontSize = useSetRecoilState(fontSizeState)
        const fontSizeLabel = useRecoilValue(fontSizeLabelState)

        return ()
      }
      ```
