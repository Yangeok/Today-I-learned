# airflow

- hooks
  - db같은 외부 시스템과 통신하기 위한 인터페이스를 제공하고, 연결 상태를 유지
  - operator 내부에서 사용
- sensor
  - 어떤 결과를 만족하는지 외부 이벤트를 주기적으로 체크할 때 사용
- pool
  - 동시에 dag를 실행할 수 있는 숫자 (기본값은 128)
  - 동시에 실행이 불가능한 경우, priority_weight 옵션으로 먼저 수행할 task의 우선 순위 지정 가능
- trigger rules
  - all_success: 이전 task 전체가 성공한 경우
  - all_failed: 이전 task 전체 또는 직전 task가 실패한 경우
  - all_done: 이전 task 실행이 모두 완료된 경우
  - one_failed: 이전 task가 1개 이상 실패한 경우
  - one_success: 이전 task가 1개 이상 성공한 경우
  - none_failed: 이전 task에 실패가 없는 경우
  - none_failed_min_one_success: 이전 task에 실패가 없고 최소한 1개 이상 성공한 경우
  - none_skipped: 이전 task에 스킵 상태가 없는 경우
  - always: 항상 실행
