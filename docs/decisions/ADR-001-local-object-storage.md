# ADR-001: 로컬 오브젝트 스토리지로 SeaweedFS 선택

- 상태: 확정
- 날짜: 2026-10-25

## 배경
초기 계획은 로컬 S3 대용으로 MinIO를 쓰는 것이었다.
docker compose up 시 minio/minio 이미지를 pull할 수 없었고,
quay.io/minio/minio도 동일하게 실패했다.
조사 결과 MinIO 커뮤니티 에디션이 종료(아카이브)되어 공식 이미지가 공개 배포되지 않는 상태였다.

## 결정
로컬 S3 호환 스토리지를 SeaweedFS(chrislusf/seaweedfs)로 교체한다.
애플리케이션은 MinIO 전용 SDK가 아니라 AWS SDK v2(S3 API)에 의존한다.

## 검토한 대안
| 대안 | 판단 |
|---|---|
| Garage | 가볍지만 설정 파일 작성 부담. 학습용으로는 SeaweedFS가 간편 |
| RustFS | 비교적 신생, 안정성 검증 부족 |
| MinIO 소스 빌드 | Go 빌드 환경 관리가 프로젝트 본질에서 벗어남 |
| MinIO 포크 | 검증 부족 |

## 결과
- 특정 벤더 SDK가 아니라 S3 API 표준에 의존하므로 구현체 교체 비용이 낮다.
- 17주차 AWS S3 전환 시 엔드포인트와 키만 변경하면 된다.
- 교훈: 외부 오픈소스 의존성은 표준 API 뒤에 두면 교체 리스크를 흡수할 수 있다.