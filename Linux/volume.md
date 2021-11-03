# home, root 영역 볼륨 조정

- `/home` 디렉토리 압축 및 백업

```sql
tar -zcf /home.tar.gz -C /home .
```

- 파일시스템명 확인 및 home 언마운트

```sql
df -hT
# Filesystem     Type      Size  Used Avail Use% Mounted on
# /dev/vda1      ext4       16G  5.6G  9.8G  37% /
# /dev/vda2      ext4       32G  1G    31G   85% /home

umount /dev/vda2
```

- 논리 볼륨 home 삭제

```sql
lvremove /dev/vda2
```

- root에 남은 용량 모두 할당

```sql
lvextend -r -l +100%FREE /dev/vda1
```

- `/home` 생성 및 복구

```sql
mkdir /home
tar -zcf /home.tar.gz -C /home
```
