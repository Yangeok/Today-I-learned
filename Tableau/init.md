# Tableau Server 초기화

- 모든 관련 패키지를 모아 설치한 다음 다음과 같이 `root` 계정으로  `tsm start`를 하면 일반계정이 필요하다고 나온다
- 다음과 같이 사용자를 추가한다

```sh
useradd USERNAME
passwd USERNAME
su - USERNAME
```

- `sudo`를 일반 사용자에게도 열어주기 위해 `wheel` 그룹에 넣거나 `sudoers` 파일을 수정해야 하는데 후자를 선택하겠다

```bash
## Allow root to run any commands anywhere
root ALL=(ALL) ALL
USER ALL=(ALL:ALL) ALL
```

- 추가한 사용자로 로그인해서 다음과 같이 `tsm`을 시작한다

```bash
sudo /opt/tableau/tableau_server/packages/scripts.VERSION/initialize-tsm --accepteula
```

- 해당 명령을 실행하면 자동으로 `tsmadmin` 그룹에 사용자가 추가되고, `tableau` 계정이 생성된다
- GUI인 `https://USERNAME:8850`에 접속해서 tableau server용 라이센스를 추가한다
- 다음과 같이 `tabadmin`도 활성화시킨다

```bash
tabcmd initialuser —server [http://localhost](http://localhost) —username USERNAME
```