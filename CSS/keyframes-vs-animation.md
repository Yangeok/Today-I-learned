# keyframe vs. animation

- keyframes
  - 타임라인 안의 하나의 구간이라고 생각할 수 있다.
  - `@keyframes`로 셀렉터를 묶어주면 된다.
  - keyframes를 사용하기 위해서는 아래와 같은 3가지가 필요하다.
    - animation-name: 사용자가 직접 지정한 이름으로, `@keyframes`가 적용될 애니메이션의 이름이다.
    - stage: from-to 혹은 0-100%의 구간이다.
    - css style: 각 스테이지에 적용시킬 스타일이다.

    ```css
    /* way 1 */
    @keyframes div {
      0% {
        opacity: 1;
      }
      100% {
        opacity: 0;
      }
    }

    /* way 2 */
    @keyframes div {
      from {
        opacity: 1;
      }
      to {
        opacity: 0;
      }
    }
    
    /* way 3 */
    @keyframes div {
      to {
        opacity: 0;
      }
    }
    ```

- animation
  - keyframe과 같은 용도지만 어떤 클래스 안에서 여러가지 속성으로 분리해서 사용할 수 있다.
