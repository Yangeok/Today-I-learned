# 용어 정리

- unsigned
  - int 필드의 경우 범위가 `-2147483648`부터 `2147483648`까지이다.
  - 음수의 범위를 양수로 옮겨 `0`부터 `4294967295`로 바꿀 수 있는 옵션이다.
- constraint
  - pk: `ALTER TABLE {table_name} ADD CONSTRAINT PRIMARY KEY {column_name};`
  - fk
  ```sql
  ALTER TABLE {table_name} 
  ADD CONSTRAINT {constraint_name} 
  FOREIGN KEY {column_name} 
  REFERENCES {parent_table_name} {pk_column_name}
  ON DELETE CASCADE;

  -- or
  ON UPDATE CASCADE;
  ```
  - not null: `ALTER TABLE {table_name} MODIFY {column_name} {data_type} CONSTRAINT {constraint_name} NOT NULL;`
  - 제약조건 확인: `SELECT * FROM {table_name}.table_constraint;`
  - 제약조건 삭제: `ALTER TABLE {table_name} DROP CONSTRAINT {constraint_name};`
