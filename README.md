# SubFlow
Job 기반 AI 미디어 자막 서비스 (Spring Boot + Python Worker)

## Tech Stack
- Backend: Java 17, Spring Boot 4.x, Gradle 8.14
- DB: PostgreSQL 16
- Queue: Redis 7 (2단계에서 사용)
- Object Storage: SeaweedFS (S3 호환, 로컬 개발용)
- Infra: Docker Compose

## 로컬 실행
1. 환경변수 파일 생성  
프로젝트 루트 디렉터리에서 실행합니다.
```
    cp .env.example .env
```
2. PostgreSQL 실행
```
    docker compose up -d
    docker compose ps        # postgres/redis healthy 확인
```
3. DB비밀번호는 환경변수로 터미널환경에 설정 후 Spring Boot 실행  
    - PowerShell:
```
     cd backend
     $env:POSTGRES_PASSWORD="<password>"
     .\gradlew.bat bootRun
```
- IntelliJ: Run Configuration > Environment variables에 `POSTGRES_PASSWORD=<password>` 추가
4. 서버 상태 확인
```
   curl.exe http://localhost:8080/actuator/health
   # {"status" : "UP"}
```

## Progress
- [x] Level 1: Spring Boot + PostgreSQL
- [x] Level 2: Docker / Docker Compose
- [ ] Level 3: File Storage (S3 호환)
- [ ] Level 4: Redis + Async Job
- [ ] Level 5: Python Worker
- [ ] Level 6: Whisper (FFmpeg)
- [ ] Level 7: Subtitle QC
- [ ] Level 8: Converter (SRT/VTT)
- [ ] Level 9: 배포 (EC2 + CI/CD)