# PKI(Public Key Infrastructure)란

- PKI를 이해하기 위해 이해하고 있어야 할 것은 다음과 같다
  - 해시함수(Messagage Digest)가 주로 하는 일은 메시지 축약이다. 긴 파일도 간단하게 축약시킬 수 있다

  - 대칭키
    - 암호화, 복호화시 1개의 같은 키를 사용한다
    - AES가 대표적인 알고리즘으로 속도가 빠른 편이다
  - 비대칭키
    - 키를 2개를 사용해서 대칭이 아니므로 비대칭키라고 부른다
    - RSA가 대표적인 알고리즘이다
    - 공개키로 암호화하는 경우는 평문을 암호화하기 위한 목적이다
    - 개인키로 암호화하는 경우는 개인키를 개인만 가지고 있고, 공개키는 대중에게 공개됐다는 가정 하에 내용을 증명하기 위해 사용한다. 이 경우 전자서명(개인키), 서명 검증(공개키)로 불린다
