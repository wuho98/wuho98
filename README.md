# 차우호 | Backend Developer

약 3년간 SW QA로 문제의 재현 조건과 기대 결과를 정리해 왔습니다. 이제는 Java와 Spring을 기반으로 문제의 원인을 분석하고, 테스트와 실행 지표로 개선 결과를 검증하는 백엔드 개발자로 성장하고 있습니다.

## What I focus on

- Redis 원자 연산과 TTL을 이용해 동시 요청의 중복 처리를 먼저 차단하고, DB 제약을 최종 정합성 방어선으로 둡니다.
- 분산 락의 범위와 트랜잭션 시작 순서를 분리해 다중 인스턴스에서도 지켜야 할 불변식을 코드로 표현합니다.
- 쿼리 수, 실행 계획, p95 같은 지표를 동일한 조건에서 비교하고 재현 가능한 테스트·스크립트를 남깁니다.
- AI는 요구사항 정리와 반복 작업을 보조하는 도구로 사용하고, 완료 기준과 테스트를 통해 생성된 결과를 직접 검증합니다.

## Featured Projects

### Error Alert

오류 이벤트를 수집하고 최근 60초 급증을 감지해 Webhook 알림을 보내는 백엔드 시스템입니다.

- Redis Lua + ZSET 기반 최근 60초 원자 집계
- `SET NX + TTL`로 임계값 이상 991개 요청의 DB INSERT 시도를 `991 → 1`로 감소
- DB Unique 제약을 최종 정합성 방어선으로 유지
- Testcontainers 동시성 테스트와 Playwright API E2E

→ [프로젝트와 검증 근거 보기](https://github.com/wuho98/error-alert-portfolio)

### PlayOn / SportTeam

시설 예약, 팀 매칭, 참가비 결제·환불과 실시간 알림을 연결한 생활 스포츠 매칭 플랫폼입니다.

- 매칭 생성·참가·확정·취소와 조회 담당
- `matchId` 단위 Redisson 분산 락과 락 획득 후 트랜잭션 시작 구조
- k6 참가 부하 테스트 스크립트
- 복합 인덱스로 대표 조회의 실제 읽은 row `10,000 → 20`, 실행 시간 `약 10ms → 1.36ms`

→ [프로젝트와 검증 근거 보기](https://github.com/prgrms-be-devcourse/NBE9-11-final-Team02)

### Book Community

도서·전자책 판매와 판매자 피드 커뮤니티를 결합한 백엔드 프로젝트입니다.

- 피드·댓글·좋아요와 S3 Presigned URL 이미지 업로드
- Java 구현을 Kotlin으로 점진 전환
- 댓글 20개의 좋아요 여부를 댓글별 조회 대신 한 번에 조회해 관련 SQL `20 → 1`
- 서비스·컨트롤러 테스트로 정상·예외 흐름 검증

→ [Kotlin 프로젝트와 검증 근거 보기](https://github.com/prgrms-be-devcourse/NBE9-11-3-Team10-BE) · [이전 Java 구현](https://github.com/prgrms-be-devcourse/NBE9-11-2-Team10-BE)

## How I verify

```text
문제 재현 → 병목·불변식 정의 → 대안 비교 → 구현 → 정상·예외·동시성 테스트 → 지표 확인
```

README의 수치는 저장소에 코드, 테스트 또는 측정 문서가 있는 항목만 사용합니다. 실행 환경에 따라 달라지는 값은 측정 조건과 함께 기록합니다.

## Tech Stack

`Java` `Kotlin` `Spring Boot` `JPA` `QueryDSL` `MySQL` `Redis` `Redisson` `Kafka`

`JUnit 5` `Testcontainers` `k6` `Playwright` `Docker` `AWS S3` `Prometheus` `Grafana`
