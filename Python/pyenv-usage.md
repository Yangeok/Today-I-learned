# pyenv, pyenv-virtualenv 사용하기

- 설치는 아래와 같이 한다

```bash
# macos
brew install pyenv pyenv-virtualenv

# linux
curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash
```

- 환경변수를 생성한다

```bash
# macos
export PYENV_ROOT=/usr/local/var/pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi

# linux
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

- 아래와 같이 python 버전을 설정하기 위한 명령어를 사용할 수 있다
  - `pyenv install —list`: 설치할 수 있는 python 버전을 확인
  - `pyenv install <version name>`: 특정 버전 설치
  - `pyenv uninstall <version name>`: 특정 버전 삭제
  - `pyenv versions`: 설치된 버전 확인
- 아래와 같이 가상환경을 설정하기 위한 명령어를 사용할 수 있다
  - `pyenv virtualenv <version> <venv name>`: 해당 버전에 가상환경 생성
  - `pyenv uninstall <venv name>` : 가상환경 삭제
  - `pyenv local <venv name>` (=`pyenv activate <venv name>)`: 가상환경 지정
  - `pyenv deactivate`: 가상환경 해제
