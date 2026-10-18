# 협업 규칙

혼자 개발하더라도 팀 프로젝트와 똑같이 진행한다. 히스토리만 봐도 "무엇을, 왜" 했는지 보이게 하는 게 목적.

## 1. 작업 흐름 (GitHub Flow)

```
이슈 생성 → 브랜치 생성 → 커밋 → PR → 리뷰 → CI 통과 → Squash merge → 브랜치 삭제 → 이슈 자동 종료
```

- `main` 은 항상 빌드·테스트가 통과하는 상태. **직접 push 금지** (브랜치 보호).
- 이슈 하나 = 브랜치 하나 = PR 하나. PR은 작게 (변경 300줄 이하 권장).

## 2. 브랜치 이름

`타입/#이슈번호-짧은-설명`

| 타입 | 용도 | 예시 |
|---|---|---|
| `feature` | 새 기능 | `feature/#5-jwt-login` |
| `fix` | 버그 수정 | `fix/#21-duplicate-order` |
| `refactor` | 동작 변경 없는 구조 개선 | `refactor/#30-order-service` |
| `docs` | 문서 | `docs/#4-erd` |
| `chore` | 설정, 빌드, 의존성 | `chore/#1-project-setup` |
| `test` | 테스트만 추가 | `test/#15-cash-account-concurrency` |

## 3. 커밋 메시지

```
타입: 무엇을 했는지 (#이슈번호)

(선택) 왜 했는지, 무엇이 달라졌는지
```

| 타입 | 의미 |
|---|---|
| `feat` | 기능 추가 |
| `fix` | 버그 수정 |
| `refactor` | 리팩터링 |
| `test` | 테스트 |
| `docs` | 문서 |
| `chore` | 설정·빌드 |

예: `feat: 예수금 hold/release 구현 (#14)`

- 한 커밋에는 한 가지 일만. "코드 중간 정리", "WIP" 같은 메시지는 쓰지 않는다.
- 작업 중 커밋이 지저분해도 괜찮다. **Squash merge** 하면 main에는 PR 제목 하나로 남는다.

## 4. Pull Request

- 제목: 커밋 메시지 규칙과 같게. 예: `feat: JWT 로그인 구현 (#5)`
- 본문: PR 템플릿(무엇을 / 왜 / 어떻게 테스트했나) 채우기. `Closes #5` 를 넣으면 merge 시 이슈가 자동으로 닫힌다.
- 리뷰: Claude에게 PR 링크나 브랜치 이름을 주고 리뷰 요청 → 코멘트 반영 후 merge.
- merge 방식: **Squash and merge** 만 사용.

## 5. 라벨

| 라벨 | 의미 |
|---|---|
| `feature` | 새 기능 |
| `bug` | 버그 |
| `refactor` | 리팩터링 |
| `docs` | 문서 |
| `chore` | 설정 |
| `troubleshooting` | 트러블슈팅 기록 대상 (포트폴리오에 쓸 것) |

## 6. 트러블슈팅 기록

`troubleshooting` 라벨 이슈를 끝내면 `docs/troubleshooting/번호-제목.md` 를 [템플릿](troubleshooting/TEMPLATE.md)으로 작성해서 같은 PR에 포함한다.
