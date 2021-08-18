# wheel 그룹에서 su 명령어 사용하기

- `/usr/bin/su`, `/bin/su`의 권한을 `4750`으로 변경한다 (최초에는 `4755`, `rwsr-xr-x`)

    ```bash
    chmod 4750 /usr/bin/su
    chmod 4750 /bin/su
    ```

- `/bin/su`의 명령어 그룹을 변경한다

    ```bash
    chgrp wheel /bin/su
    ```

- wheel 그룹에 일반계정을 추가한다

    ```bash
    # way 1
    gpasswd -a <account_name> wheel

    # way 2
    usermod -aG wheel <account_name>
    ```

- `/etc/pam.d/su` 파일에서 명시적으로 wheel 그룹 내 사용자들을 신뢰하는 구문의 주석을 해제한다

    ```bash
    # Uncomment the following line to implicitly trust users in the "wheel" group.
    #auth           sufficient      pam_wheel.so trust use_uid
    ```