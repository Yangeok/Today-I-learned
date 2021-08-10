# MariaDB 쿼리 모니터링

- 로그 활성화

```sql
SET GLOBAL general_log='ON';
SET GLOBAL slow_query_log='ON';
SET GLOBAL log_output='TABLE';
```

- 로그 테이블을 통해 실행한 쿼리를 확인

```sql
SELECT * FROM mysql.general_log gl;
```

- 로그기능 비활성화

```sql
SET GLOBAL general_log='OFF';
SET GLOBAL slow_query_log='OFF';
SET GLOBAL log_output='NONE';
```