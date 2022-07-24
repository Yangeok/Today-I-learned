# iv란

- iv(Initialization Vector, 초기화 벡터)
  - 블럭 암호화인 CBC(Chiper Block Chaining mode)에서 사용하여 첫 블럭이 다음 암호화 블럭에 영향을 미친다
  - key와는 다른 개념으로 iv는 시작시 값과 암호화 후 값을 보면 달라진다
  - 주의할 점으로 iv값을 복호화할 경우 반드시 최초값과 동일하게 설정해야 한다
