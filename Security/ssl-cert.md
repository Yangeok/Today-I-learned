# SSL 인증서란

- SSL 인증서는 CA(Certificate AUthority, 인증 기관)에서 시작하는 Root 인증서에서 시작한다
- 일반적으로 인증서는 Root, Intermediate(중간 인증서), Leaf(서버 인증서) 3단계로 구성되어있고, 이를 인증서 체인이라고 부른다
- 사용자가 구입하는 SSL 인증서는 Leaf 인증서를 의미하며, 인증서 체인의 일부이다
- 인증서 체인은 하위 인증서에 서명하고, 상위 인증서를 참고하는 방식으로 만들어진다
- 서버의 인증서를 신뢰하려면 해당 서명을 Root CA로 추적이 가능해야 한다

<img src="[https://img1.daumcdn.net/thumb/R1280x0.fjpg/?fname=http://t1.daumcdn.net/brunch/service/user/JqQ/image/5lULic9oG815Nalhj1mafGl9ibk](https://img1.daumcdn.net/thumb/R1280x0.fjpg/?fname=http://t1.daumcdn.net/brunch/service/user/JqQ/image/5lULic9oG815Nalhj1mafGl9ibk)">

- Root CA 인증서는 웹브라우저의 특정 저장소에 포함되어 있다
- 일부 OS에는 사전 설치되어서 따로 다운받을 필요가 없다
- Root 인증서를 발급한 기관이 신뢰할 수 있는 Root CA 목록에 없으면 신뢰할 수 있는 인증서가 아니라고 경고가 표시된다

<img src="[https://img1.daumcdn.net/thumb/R1280x0.fjpg/?fname=http://t1.daumcdn.net/brunch/service/user/JqQ/image/ZiTAOAFpCFHmS_IG9P28lzcggzE.jpg](https://img1.daumcdn.net/thumb/R1280x0.fjpg/?fname=http://t1.daumcdn.net/brunch/service/user/JqQ/image/ZiTAOAFpCFHmS_IG9P28lzcggzE.jpg)">

- 인증서에는 다음과 같은 내용들이 포함되어 있다
    - 인증서 소유자의 이름
    - 인증서 소유자의 공개키 (비밀키는 CA가 소유)
    - 인증서의 유효기간
    - 고유한 UID
    - 인증서의 기타 모든 값들을 해시한 값