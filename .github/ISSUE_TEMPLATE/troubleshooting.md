---
name: 트러블슈팅
about: 일부러 재현하고 해결할 문제 (포트폴리오 기록 대상)
title: "fix: [TS#번호] "
labels: troubleshooting
---

## 문제 상황
예: 주문 응답이 타임아웃 났는데 실제로는 증권사에 주문이 들어가 있어서, 재시도하면 중복 주문이 생긴다.

## 재현 계획
예: `fake-broker.accept-then-timeout-rate: 0.3`, 주문 100건 → 중복 주문 수 측정

## 해결 후보
- A:
- B:

## 완료 조건
- [ ] 전/후 수치 측정
- [ ] 재현 테스트 코드
- [ ] `docs/troubleshooting/` 기록
