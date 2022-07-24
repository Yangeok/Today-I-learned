# PostgreSQL 메타 쿼리

- 데이터베이스 목록 보기

    ```sql
    SELECT DATNAME FROM PG_DATABASE WHERE DATNAME LIKE '데이터베이스명';
    ```

- 테이블 목록 보기

    ```sql
    SELECT RELNAME AS TABLE_NAME FROM PG_STAT_USER_TABLES
    ```

- 테이블 커멘트 보기

    ```sql
    SELECT PS.RELNAME AS TABLE_NAME, PD.DESCRIPTION AS TABLE_COMMENT
    FROM  PG_STAT_USER_TABLES PS, PG_DESCRIPTION PD
    WHERE PS.RELNAME  = '테이블명'
    AND PS.RELID = PD.OBJOID
    AND PD.OBJSUBID = 0
    ```

- 테이블별 라인수 보기

    ```sql
    SELECT
      pgClass.relname   AS tableName,
      pgClass.reltuples AS rowCount
    FROM
      pg_class pgClass
    INNER JOIN
      pg_namespace pgNamespace ON (pgNamespace.oid = pgClass.relnamespace)
    WHERE
      pgNamespace.nspname NOT IN ('pg_catalog', 'information_schema') AND
      pgClass.relkind='r'
    ```

- 스키마, 테이블 목록 보기

    ```sql
    SELECT SCHEMANAME AS SCHEMA_NAME, TABLENAME AS TABLE_NAME
    FROM PG_CATALOG.PG_TABLES 
    WHERE SCHEMANAME != 'PG_CATALOG' AND SCHEMANAME != 'INFORMATION_SCHEMA';
    ```

- 칼럼 커멘트 보기

    ```sql
    SELECT 
      PS.RELNAME AS TABLE_NAME,
      PA.ATTNAME AS COLUMN_NAME,
      PD.DESCRIPTION AS COLUMN_COMMENT
    FROM 
      PG_STAT_ALL_TABLES PS,
      PG_DESCRIPTION PD,
      PG_ATTRIBUTE PA
    WHERE PS.SCHEMANAME = (
      SELECT SCHEMANAME
      FROM PG_STAT_USER_TABLES
      WHERE RELNAME = '테이블명'
    )
    AND PS.RELNAME = '테이블명'
    AND PS.RELID = PD.OBJOID
    AND PD.OBJSUBID <> 0
    AND PD.OBJOID = PA.ATTRELID
    AND PD.OBJSUBID = PA.ATTNUM
    ORDER BY PS.RELNAME, PD.OBJSUBID
    ```
