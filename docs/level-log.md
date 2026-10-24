## Level 1: Spring Boot + PostgreSQL
- 도입 이유: Job/MediaFile 메타데이터를 저장할 RDB가 필요
- 결과: Hikari 연결 확인, actuator health가 DB 상태를 반영함

## Level 2: Docker Compose 도입
- 도입 이유: Redis, Worker, 스토리지까지 붙일 예정이라 "내 PC에서만 되는 환경"을 방지
- 도입 전 예상 문제: 인프라별 로컬 설치 버전 불일치, 환경 재현 불가
- 결과: docker compose up 한 번으로 인프라 기동.
  단, 외부 이미지 의존성 리스크를 직접 겪음 (-> ADR-001)