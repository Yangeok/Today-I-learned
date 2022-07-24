# 코드포매팅 자동화하기

- 아래와 같이 설치한다

```bash
pip install black pre-commit
```

- cli로 파일마다 실행할 수도 있다

```bash
black index.py
```

- pre commit 깃훅 설정
  - `.pre-commit-config.yml` 에 다음과 같은 설정을 추가한다

        ```bash
        repos:
          - repo: https://github.com/psf/black
            rev: stable
            hooks:
              - id: black
        ```

  - `pre-commit` 커맨드로 방금 작성한 깃훅 스크립트를 설치한다

        ```bash
        pre-commit install
        ```
