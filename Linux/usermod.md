# usermod 명령어

- `usermod`는 `/usr/sbin`에 포함되어 있어서 root 계정으로만 접근이 가능하다
- 우선 사용자 계정을 변경할 수 있는 `usermod`를 사용하기 전에 사용자를 추가하는 `useradd`는 다음과 같은 특성이 있다
  - `/etc/default/useradd` 파일을 참조한다
  - 이 파일에 의해 사용자를 생성하면 `/home/<username>` 폴더가 생성된다
- `-d <will_be_changed_loc> -m <username>`: 바꿀 위치에 디렉토리를 만들지 않아도, `/home/<username>` 폴더를 원하는 위치에 권한을 그대로 옮길 수 있다
- `-u <uid> <username>`: 사용자의 UID를 변경한다. UID를 0으로 변경하면 root의 권한을 가질 수 있다
- `-G <group_name[, group_name2...]>`: 2차 그룹을 지정할 수 있다. 복수개의 그룹을 컴마 구분자로 지정할 수 있다
- `-s <shell_loc> <username>`: 원하는 쉘을 사용자에 지정할 수 있다
- `-e <yyyy-mm-dd> <username>`: 계정의 만료일을 지정할 수 있다
- `-l <will_be_changed_name> <username>`: 사용자 이름을 바꿀 수 있다
