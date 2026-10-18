# 00. 시작 가이드 (처음 한 번)

## 1. 첫 커밋 (터미널, ~/projects/stock-trading)

```bash
cd ~/projects/stock-trading
git init -b main
git add .
git status          # secret.yml, data/ 가 없는지 확인
git commit -m "docs: 기획 문서와 협업 규칙, GitHub 템플릿 추가"
```

## 2. GitHub 저장소 만들고 올리기

1. github.com → New repository → 이름 `stock-trading`, **Public**, README/.gitignore 추가하지 않기 (이미 있음).
2. 터미널:
```bash
git remote add origin https://github.com/<내아이디>/stock-trading.git
git push -u origin main
```
3. Actions 탭에서 CI가 초록색인지 확인 (아직 Gradle 프로젝트가 없어서 빌드는 건너뜀).

## 3. 저장소 설정

| 메뉴 | 설정 |
|---|---|
| Settings → General → Pull Requests | **Allow squash merging만** 체크, "Automatically delete head branches" 체크 |
| Settings → Branches → Add rule (`main`) | Require a pull request before merging, Require status checks to pass (`build`) |
| Issues → Labels | `feature`, `bug`, `refactor`, `docs`, `chore`, `troubleshooting` 만들기 |
| Issues → Milestones | `M1 기반` ~ `M6 확장` 6개 만들기 |
| Projects → New project → Board | Todo / In Progress / Done, 저장소 연결 |

> 혼자라서 "Require approvals"는 끄기 (본인 PR은 본인이 승인 못 함). 리뷰는 Claude에게 받고 코멘트로 남긴다.

## 4. 이슈 등록

[04-backlog.md](04-backlog.md)를 보고 **M1, M2 이슈만 먼저** 등록 (#1~#6). 나머지는 마일스톤에 들어갈 때 등록해도 된다.

## 5. 첫 작업 (#1)

```bash
git switch -c chore/#1-project-setup
# 기존 프로젝트의 build.gradle, settings.gradle, gradle/, gradlew* 를 참고해서 옮기고
# StockTradingApplication + contextLoads 테스트만 있는 상태로 ./gradlew build 성공시키기
git add . && git commit -m "chore: Spring Boot 프로젝트 생성 (#1)"
git push -u origin chore/#1-project-setup
```
GitHub에서 PR 생성 → 본문에 `Closes #1` → CI 통과 확인 → Claude 리뷰 → Squash merge.
