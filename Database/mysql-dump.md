# MySQL 덤프

- 덤프하기

```bash
mysqldump -u [USERNAME] -p [DATABASE] > [FILENAME]
```

- 원하는 테이블만 덤프하기

```bash
mysqldump -u [USERNAME] -p [DATABASE] [TABLENAME] > [FILENAME]
```

- 복구하기

```bash
mysql -u [USERNAME] -p [DATABASE] < [FILENAME]
```