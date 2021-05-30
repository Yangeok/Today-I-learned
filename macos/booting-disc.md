# 맥OS에서 부팅 디스크 굽기

- 디스크 유틸리티에서 usb 포맷학기
- 터미널에서 diskutil로 디스크 위치를 확인한다

```bash
diskutil list
```

- 디스크를 언마운트한다

```bash
diskutil unmountDisk /dev/disk2
```

- `.iso` 파일을 usb로 복사한다

```bash
sudo dd if=rhel-server-7.8-x86_64-dvd.iso of=/dev/disk2
```

- 진행상황은 `ctrl + t`로 확인할 수 있다

```bash
load: 1.95  cmd: dd 20536 uninterruptible 6.46u 56.07s
3577265+0 records in
3577264+0 records out
1831559168 bytes transferred in 1441.749715 secs (1270372 bytes/sec)
```