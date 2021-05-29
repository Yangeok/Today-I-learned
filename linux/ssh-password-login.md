## login ssh with password

- ssh 공개키를 복사해서 ~/.ssh/authorized_keys로 옮긴다

```bash
cd .ssh
cat key.pub | pbcopy
```

- ssh 권한없음 에러가 발생하는 경우 원격 서버의 ssh 파일 및 폴더 권한 설정을 변경한다

```bash
chmod 700 /root/.ssh
chmod 600 /root/.ssh/authorized_keys
```

- `sshd_config` 파일에 아래와 같은 설정을 추가한다

```bash
sudo sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/g' /etc/ssh/sshd_config;
sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config;
```

- `sshd` 서비스를 재시작한다

```bash
systemctl stop sshd.service
systemctl enable sshd.service
systemctl start sshd.service
systemctl status sshd.service
```

- `scp`에 사용할 `ssh` 사용자 비밀번호를 설정한다

```bash
sudo su
passwd USER
```

- `/etc/sudoers`를 수정한다

```bash
## Allow root to run any commands anywhere
root ALL=(ALL) ALL
USER ALL=(ALL:ALL) ALL

## Same thing without a password
# %wheel ALL=(ALL) NOPASSWD: ALL
%admin ALL=(ALL) ALL

## Allows members of the users group to mount and unmount the
## cdrom as root
# %users  ALL=/sbin/mount /mnt/cdrom, /sbin/umount /mnt/cdrom
%sudo ALL=(ALL:ALL) ALL
```