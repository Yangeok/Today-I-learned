# RHEL 정품인증

- [RHSM 웹페이지 > 시스템](https://access.redhat.com/management/systems) 에서 프로파일을 새로 만든다
- `entitlement_certificates/*.pem` 인증서를 다운받아서, 시스템의 `/tmp` 디렉토리로 옮긴다
- 아래와 같은 명령어로 인증서를 추가한다

```
subscription-manager import --certificate=/tmp/Name_Of_Downloaded_Entitlement_Cert.pem
```

- 인증서를 아래와 같은 명령어로 조작할 수 있다

```bash
subscription-manager remove --all # 인증서 모두 삭제
subscription-manager unregister # 인증서 삭제
subscription-manager clean # 인증서 로컬데이터 삭제
subscription-manager register # 인증서 등록 (온라인)
subscription-manager register --username <username> --password <password> --auto-attach # 고객 포탈에 등록된 인증서 등록 (온라인)
subscription-manager-gui # gui로 인증서 등록 (온라인)
subscription-manager list # 인증서 목록
```

- 라이센스 등록 여부 상세를 확인하고 싶은 경우 아래와 같이 입력할 수 있다

```jsx
subscription-manager list --consumed
```
