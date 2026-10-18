# 한국투자증권 모의투자 API 신청

| 단계 | 할 일 | 결과물 |
|---|---|---|
| 1 | 한국투자증권 계좌 개설 + 홈페이지 ID 등록 | 로그인 가능한 ID |
| 2 | 모의투자 신청 (국내주식) | 모의투자 계좌번호 |
| 3 | KIS Developers에서 API 서비스 신청 (모의투자 계좌 선택) | APP Key, APP Secret |
| 4 | `secret.yml` 에 입력 | 연동 준비 완료 |

> 메뉴 이름·절차는 바뀔 수 있으니 실제 화면과 공식 안내를 기준으로.

## 1. 계좌 개설 + ID 등록
- 한국투자증권 앱(비대면)으로 계좌 개설 → 홈페이지/앱에서 ID 등록.
- API 서비스 신청 화면에 로그인하려면 이 ID가 필요.

## 2. 모의투자 신청
- 한국투자증권 홈페이지 또는 앱의 **모의투자** 메뉴에서 국내주식 모의투자 신청.
- 발급된 **모의투자 계좌번호** 메모 (앞 8자리 = `account-no`, 뒤 2자리 = `account-product-code`, 보통 `01`).
- 모의투자는 이용 기간이 정해져 있을 수 있음 → 만료되면 재신청 (계좌번호/키가 바뀌는지 확인).

## 3. API 서비스 신청 (KIS Developers)
- https://apiportal.koreainvestment.com 접속 → 로그인 → API 신청.
- **모의투자 계좌**를 선택해서 신청 → **APP Key / APP Secret** 발급.
- 같이 확인해둘 것 (Phase 1에서 바로 필요):
  - 모의투자 REST / WebSocket 도메인 (application.yml의 `kis.base-url`, `kis.ws-url`과 비교)
  - 접근 토큰 발급 API, **토큰 유효기간과 발급 횟수 제한**
  - **초당 호출 제한** (모의투자는 실전보다 낮은 편)
  - 현재가 조회 / 주문(현금) / 일별 주문체결 조회 / 잔고 조회 API의 tr_id (모의와 실전이 다름)
- 공식 샘플 코드: GitHub `koreainvestment/open-trading-api` (Python이지만 요청 형식 참고용으로 좋음)

## 4. secret.yml 작성
```bash
cp secret.yml.example secret.yml
```
값을 채우고 `broker.type: kis` 로 바꾸면 실제 모의투자 API 사용.

## 주의
- APP Secret은 비밀번호와 같음. `secret.yml`은 `.gitignore`에 있으니 커밋되지 않는지 `git status`로 한 번 확인.
- 실수로 GitHub에 올렸다면 바로 재발급.
