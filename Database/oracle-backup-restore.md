# Oracle Backup/Restore

- 백업
  - 물리적
    - datafile, controlfile, redo log, parameter
  - 논리적
    - 테이블, 뷰, 인덱스, pl/sql 블록
- 복구
  - 노-아카이브 모드
    - 데이터베이스 설치시 기본값
    - 로그버퍼 영역과 redo log 파일에 저장된 로그를 복원
  - 아카이브 모드
