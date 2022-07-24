# csv로 sql one-to-many 관계 데이터 만들기

- 데이터를 삽입할 테이블을 만든다

```sql
CREATE TABLE Companies
(
    `id`         int(11) unsigned    NOT NULL    AUTO_INCREMENT COMMENT 'ID', 
    `name`       varchar(45)         NULL        COMMENT '제조사명', 
    `createdAt`  datetime            NOT NULL    DEFAULT current_timestamp() COMMENT '생성 일자', 
    `updatedAt`  datetime            NULL        DEFAULT current_timestamp() COMMENT '변경 일자', 
    CONSTRAINT PK_Companies PRIMARY KEY (id)
);

CREATE TABLE HealthPrds
(
    `id`          int(11) unsigned    NOT NULL    AUTO_INCREMENT COMMENT 'ID', 
    `itemSeq`     varchar(22)         NULL        COMMENT '제품 번호', 
    `companyId`   int(11) unsigned    NULL        COMMENT '제조사 ID', 
    `name`        varchar(255)        NULL        COMMENT '제품명', 
    `photo`       blob                NULL        COMMENT '이미지', 
    `total`       float               NULL        COMMENT '총량', 
    `unitId`      int(11) unsigned    NULL        COMMENT '성분 용량 단위 ID', 
    `intake`      TEXT                NULL        COMMENT '섭취방법', 
    `storage`     text                NULL        COMMENT '저장방법', 
    `expiration`  varchar(255)        NULL        COMMENT '유효기한', 
    `appearance`  TEXT                NULL        COMMENT '성상', 
    `flag`        TINYINT(1)          NULL        DEFAULT 1 COMMENT '사용 여부', 
    `createdAt`   datetime            NOT NULL    DEFAULT current_timestamp() COMMENT '생성 일자', 
    `updatedAt`   datetime            NULL        DEFAULT current_timestamp() COMMENT '변경 일자', 
    CONSTRAINT PK_HealthProducts PRIMARY KEY (id)
);
```

- 임시 테이블을 하나 만든다

```jsx
CREATE TABLE TempTable_1 (
  intake text null,
  productName varchar(255) null,
  itemSeq varchar(255) null,
  companyName varchar(255) null,
  appearance text null,
  expiration varchar(255) null,
  storage text null
)
```

- CSV를 테이블에 갖다 붓는다

```bash
intake, productName, expiration, itemSeq, storage, companyName, appearance
"1일 2회, 1회 2g 섭취", "고센난황레시틴Ⅲ", "1년", "2004001505570", "직사광선을 피하고, 서늘한 실온에서 보관", "(주)고센바이오텍", "황갈색의 액상제품"
"1일 1회, 1회 1포(5g)씩 물과 함께 섭취", "에이치씨에이매직다이어트", "2년간", "2004001507329", "직사광선을 피한 서늘한 곳에 보관", "엘라이프주식회사", "고유의 색택과 향미를 가지며 이미, 이취가 없어야 한다"
```

- `DISTINCT`를 포함해서 쿼리를 날린다

```sql
INSERT IGNORE INTO Companies(name)
SELECT DISTINCT companyName
FROM TempTable_1
```

- 외부 테이블에 `JOIN`이 필요한 경우 사용한다

```sql
INSERT IGNORE INTO HealthPrds(name, companyId, itemSeq, appearance, intake, expiration, storage)
SELECT DISTINCT
  t.productName,
  c.id,
  t.itemSeq,
  t.appearance,
  t.intake,
  t.expiration,
  t.storage
FROM TempTable_1 t
JOIN Companies c ON c.name = t.companyName
```

- 다만 `JOIN`은 데이터 양이 많으면 하지 않는게 좋고, 프로그램으로 삽입하는 것이 훨씬 속도가 빠르다
- 참조: [https://stackoverflow.com/questions/31476242/first-steps-in-moving-a-csv-to-a-mysql-relational-database-csv-structure-mys](https://stackoverflow.com/questions/31476242/first-steps-in-moving-a-csv-to-a-mysql-relational-database-csv-structure-mys)
