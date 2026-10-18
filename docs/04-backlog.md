# 04. 백로그 (마일스톤별 이슈)

표의 `#` 은 작업 순서 번호다. GitHub에서는 이슈와 PR이 번호를 같이 쓰기 때문에 실제 이슈 번호는 달라질 수 있다 → 브랜치·커밋에는 **GitHub가 붙여준 실제 번호**를 쓴다.
"기존 코드"는 `~/projects/Automated Stock Trading System` 에서 **참고해서 옮겨올** 파일. 그대로 복사하지 말고 읽고 이해한 뒤 옮긴다.

## M1. 기반

| # | 제목 | 라벨 | 기존 코드 |
|---|---|---|---|
| 1 | chore: Spring Boot 프로젝트 생성 및 CI 통과 | chore | `build.gradle`, `settings.gradle`, gradle wrapper, `application.yml` |
| 2 | feat: 공통 에러 응답(ErrorCode)과 전역 예외 처리 | feature | `global/exception/GlobalExceptionHandler` |
| 3 | chore: Clock 빈, BaseTimeEntity(createdAt/updatedAt) | chore | `global/config/ClockConfig` |

## M2. 회원·인증

| # | 제목 | 라벨 | 기존 코드 |
|---|---|---|---|
| 4 | feat: 회원가입 (BCrypt, 이메일·닉네임 중복 검사) | feature | BlogRest `MemberService` 참고 |
| 5 | feat: JWT 로그인과 인증 필터 | feature | BlogRest `JwtProvider`, `JwtAuthenticationFilter` 참고 |
| 6 | feat: 내 정보 조회 (/api/members/me) | feature | - |

## M3. 증권사 연동

| # | 제목 | 라벨 | 기존 코드 |
|---|---|---|---|
| 7 | feat: BrokerClient 인터페이스, DTO, 예외 | feature | `broker/BrokerClient`, `broker/dto/*`, `broker/exception/*` |
| 8 | feat: FakeBrokerClient (지연·거절·응답 유실 주입) | feature | `broker/fake/*` |
| 9 | feat: 증권 계좌 연결 (앱키·시크릿 암호화 저장) | feature | - |
| 10 | feat: 회원별 BrokerClient 선택 (FAKE/KIS) | feature | - |
| 11 | fix: [TS#1] KIS 토큰 발급 제한 — 토큰 저장·재사용·동시 갱신 | troubleshooting | `broker/kis/KisTokenManager` |
| 12 | feat: KIS 현재가·잔고 조회 | feature | `broker/kis/KisBrokerClient` |
| 13 | fix: [TS#2] 시세 수집 시 초당 호출 제한 초과 | troubleshooting | `marketdata/QuoteCollector`, `MarketHours` |

## M4. 주문

| # | 제목 | 라벨 | 기존 코드 |
|---|---|---|---|
| 14 | feat: Order 상태 머신과 상태 변경 이력 | feature | `order/domain/*`, `OrderTest` |
| 15 | fix: [TS#5] 동시 매수 시 잔고 초과 — 예수금 hold/release | troubleshooting | `account/domain/CashAccount`, `Position` |
| 16 | feat: 리스크 체크 (종목당 최대 금액, 하루 최대 주문 수) | feature | `risk/*` |
| 17 | feat: 주문 실행 1차 (단순 버전 + 재시도) | feature | `order/service/OrderService` |
| 18 | fix: [TS#3] 타임아웃 후 재시도로 중복 주문 — clientOrderId, UNKNOWN | troubleshooting | - |
| 19 | feat: 대조 스케줄러 (UNKNOWN 확정, 체결 수량 보정) | feature | `execution/OrderReconciliationScheduler` |
| 20 | feat: 주문 목록·상세 조회 API, 예수금·보유 종목 API | feature | `order/api/*` |

## M5. 자동매매

| # | 제목 | 라벨 | 기존 코드 |
|---|---|---|---|
| 21 | feat: 전략 등록·활성화 API, 이동평균 교차 전략 | feature | `strategy/*`, `MovingAverageCrossStrategyTest` |
| 22 | feat: TradingEngine — 장 시간에 활성 전략 실행 | feature | `trading/*` |
| 23 | fix: [TS#4] 체결 통보와 DB 상태 불일치 — 실시간 체결 통보 | troubleshooting | `execution/ExecutionListener` |
| 24 | fix: [TS#7] WebSocket 끊김 — 재연결과 누락 보완 | troubleshooting | - |

## M6. 확장

| # | 제목 | 라벨 |
|---|---|---|
| 25 | chore: MySQL(docker-compose) 전환, 락 동작 비교 | chore |
| 26 | fix: [TS#6] 서버 2대에서 스케줄러 중복 실행 — 분산 락 | troubleshooting |
| 27 | fix: [TS#8] 시세 폭주 — 처리량 측정과 개선 | troubleshooting |
| 28 | chore: 배포 (서버, 환경변수, 로그) | chore |
