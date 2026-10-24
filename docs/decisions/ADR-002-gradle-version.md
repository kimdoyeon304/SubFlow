# ADR-002: Gradle 8.14.3 고정

- 상태: 확정
- 날짜: 2026-10-25

## 배경
start.spring.io가 생성한 프로젝트가 Gradle 9.x였고, IntelliJ에서 main() 실행 시
"Could not get unknown property 'convention'" 에러가 발생했다.
IntelliJ가 주입하는 init script가 Gradle 9에서 삭제된 속성을 사용하는 것이 원인이다.

## 결정
gradle wrapper를 8.14.3으로 변경해 고정한다.

## 결과
IntelliJ 실행 에러가 해소되었다. 이후 IntelliJ가 Gradle 9를 지원하면 재검토한다.