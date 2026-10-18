# Stock Trading Service

여러 회원이 각자의 한국투자증권 **모의투자** 계좌를 연결하고, 전략을 등록하면 서버가 대신 자동매매해주는 백엔드 서비스.

> 수익률이 목표가 아니다. **외부 증권사 API가 느려지고, 끊기고, 응답을 안 줘도 주문이 꼬이지 않는 주문 시스템**을 만드는 게 목표다.

| 항목 | 내용 |
|---|---|
| 스택 | Java 25, Spring Boot 4.1.1, Spring Security + JWT, JPA, H2 → MySQL, (확장) Redis |
| 핵심 설계 | `BrokerClient` 인터페이스 + `FakeBrokerClient`(장애 주입) / `KisBrokerClient`(실제) |
| 핵심 도메인 | `Order` 상태 머신 (`UNKNOWN` 상태 포함), 예수금 묶기(hold) |
| 협업 방식 | GitHub Flow — 이슈 → 브랜치 → PR → 리뷰 → Squash merge ([규칙](docs/CONVENTION.md)) |

## 문서

| 문서 | 내용 |
|---|---|
| [00. 시작 가이드](docs/00-setup-guide.md) | 첫 커밋, GitHub 저장소·라벨·마일스톤·브랜치 보호 세팅 |
| [01. 요구사항](docs/01-requirements.md) | 기능/비기능 요구사항, MVP 범위 |
| [02. ERD](docs/02-erd.md) | 테이블 설계 |
| [03. API 명세](docs/03-api.md) | 엔드포인트 목록 |
| [04. 백로그](docs/04-backlog.md) | 마일스톤별 이슈 목록 |
| [협업 규칙](docs/CONVENTION.md) | 브랜치·커밋·PR 규칙 |
| [트러블슈팅](docs/troubleshooting/) | 문제 → 원인 → 대안 → 선택 → 결과 기록 |
| [KIS API 신청](docs/KIS_API_SETUP.md) | 모의투자 앱키 발급 절차 |

## 로드맵

| 마일스톤 | 내용 | 트러블슈팅 |
|---|---|---|
| M1 기반 | 프로젝트 세팅, CI, 공통 응답·예외 | - |
| M2 회원·인증 | 회원가입, JWT 로그인 | - |
| M3 증권사 연동 | BrokerClient, Fake/KIS, 계좌 연결, 토큰, 시세 | #1 토큰 발급 제한, #2 호출 제한 |
| M4 주문 | 상태 머신, 예수금 hold, 리스크, 주문 실행, 대조 | #3 타임아웃 후 중복 주문, #5 동시 주문 잔고 초과 |
| M5 자동매매 | 전략 등록, 매매 엔진, 실시간 체결 통보 | #4 체결 상태 불일치, #7 WebSocket 끊김 |
| M6 확장 | MySQL/Redis, 서버 2대, 부하 테스트, 배포 | #6 스케줄러 중복 실행, #8 시세 폭주 |
