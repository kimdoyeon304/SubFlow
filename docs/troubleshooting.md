## 1. MinIO 이미지 pull 실패 (pull access denied)
- 증상: docker compose up 시 minio/minio, quay.io/minio/minio 모두 pull 실패
- 원인: MinIO 커뮤니티 에디션 종료로 공식 이미지 공개 배포 중단
- 해결: SeaweedFS로 교체 (-> ADR-001)
- 재발 방지: 이미지 태그 고정, S3 표준 API(AWS SDK)에 의존

## 2. IntelliJ 실행 실패: Could not get unknown property 'convention'
- 증상: main() 실행 시 Gradle 초기화 스크립트에서 즉시 실패 (빌드 300ms대)
- 원인: Gradle 9에서 삭제된 convention 속성을 IntelliJ init script가 사용
- 해결: gradlew wrapper --gradle-version 8.14.3 (-> ADR-002)
- 임시 우회: 터미널에서 .\gradlew.bat bootRun

## 3. password authentication failed for user
- 증상: 앱 기동 실패. 연쇄적으로 "Unable to determine Dialect without JDBC metadata" 출력
- 원인 1: 환경변수(POSTGRES_PASSWORD)를 PowerShell 세션에만 설정해 IntelliJ 프로세스에 전달되지 않음
  -> IntelliJ Run Configuration의 Environment variables에 추가
- 원인 2: POSTGRES_PASSWORD는 볼륨 최초 생성 시에만 적용됨.
  .env를 나중에 수정하면 DB 내 비밀번호와 불일치
  -> ALTER USER로 동기화하거나, 초기 단계면 docker compose down -v 후 재기동
- 교훈: Dialect 에러는 DB 접속 실패의 2차 증상. 첫 번째 Caused by를 먼저 본다.
  컨테이너 healthy는 "DB가 떠 있다"일 뿐 "비밀번호가 맞다"가 아니다.