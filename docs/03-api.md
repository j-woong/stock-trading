# 03. API 명세 (초안)

## 핵심 키워드

| 키워드 | 한 줄 설명 |
|---|---|
| 공개 경로 | `/api/auth/**` 만 인증 없이 접근 |
| `/me` | 로그인한 회원 본인 리소스. URL에 회원 id를 넣지 않는다 |
| 에러 응답 | `{ "code": "ORDER_NOT_FOUND", "message": "..." }` 형태로 통일 |

| 기능 | Method | URL | 인증 | 마일스톤 |
|---|---|---|---|---|
| 회원가입 | POST | `/api/auth/signup` | - | M2 |
| 로그인 (JWT 발급) | POST | `/api/auth/login` | - | M2 |
| 내 정보 | GET | `/api/members/me` | O | M2 |
| 증권 계좌 연결 | PUT | `/api/members/me/broker-account` | O | M3 |
| 증권 계좌 조회 (키 제외) | GET | `/api/members/me/broker-account` | O | M3 |
| 증권 계좌 연결 테스트 | POST | `/api/members/me/broker-account/test` | O | M3 |
| 현재가 조회 | GET | `/api/quotes/{stockCode}` | O | M3 |
| 예수금 조회 | GET | `/api/members/me/cash` | O | M4 |
| 보유 종목 | GET | `/api/members/me/positions` | O | M4 |
| 주문하기 | POST | `/api/orders` | O | M4 |
| 내 주문 목록 (페이징) | GET | `/api/orders?page=1&size=20&status=` | O | M4 |
| 주문 상세 (이력 포함) | GET | `/api/orders/{id}` | O | M4 |
| 전략 등록 | POST | `/api/strategies` | O | M5 |
| 내 전략 목록 | GET | `/api/strategies` | O | M5 |
| 전략 활성/비활성 | PATCH | `/api/strategies/{id}/active` | O | M5 |
| 전략 삭제 | DELETE | `/api/strategies/{id}` | O | M5 |

## 요청/응답 예시

### POST /api/orders
```json
{ "stockCode": "005930", "side": "BUY", "quantity": 10, "price": 71000 }
```
```json
{
  "id": 42,
  "clientOrderId": "3f2c...",
  "stockCode": "005930",
  "side": "BUY",
  "quantity": 10,
  "price": 71000,
  "filledQuantity": 0,
  "status": "SUBMITTED"
}
```

### 주문 관련 에러

| 상황 | HTTP | code |
|---|---|---|
| 주문 가능 금액 부족 | 400 | `INSUFFICIENT_CASH` |
| 종목당 최대 금액 초과 | 400 | `RISK_MAX_AMOUNT_EXCEEDED` |
| 하루 최대 주문 수 초과 | 429 | `RISK_DAILY_LIMIT_EXCEEDED` |
| 증권 계좌 미연결 | 400 | `BROKER_ACCOUNT_NOT_CONNECTED` |
| 증권사 거절 | 422 | `BROKER_REJECTED` |
| 남의 주문 조회 | 404 | `ORDER_NOT_FOUND` (존재 여부를 숨김) |
