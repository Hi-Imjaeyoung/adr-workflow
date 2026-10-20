# 아키텍처 결정 기록(ADR)

이 디렉터리에는 중요한 기술적 결정을 오래 보존할 기록으로 저장합니다.

## 파일 이름 규칙

`ADR-NNN-short-kebab-case-title.md` 형식을 사용합니다. 예:

- `ADR-001-content-storage-model.md`
- `ADR-002-authentication-session-strategy.md`

ID는 순차적으로 부여합니다. ADR이 기각되거나 대체되더라도 ID를 재사용하지 않습니다.

## 상태

- `Proposed`: 논의 중이며 최종 결정이 없음.
- `Accepted`: 결정 책임자가 선택을 승인함.
- `Rejected`: 제안을 검토한 뒤 기각함.
- `Superseded`: 이후의 ADR이 이 결정을 대체함.
- `Deprecated`: 더 이상 적용되지 않음.

## 작성 가이드

- 원래 논의에 참여하지 않은 미래의 팀원을 위해 작성합니다.
- 무엇을 구현했는지뿐 아니라 왜 그렇게 선택했는지를 기록합니다.
- 확인된 사실을 가정 및 측정값과 구분합니다.
- 기록은 간결하게 유지하고, 구현 세부 사항은 이슈/PR 링크로 연결합니다.
- 승인된 결정이 실질적으로 바뀌면 새 ADR을 만들고 두 기록을 서로 연결합니다.
- ADR에 자격 증명, 비밀 값, 개인 정보, 민감한 운영 환경 정보를 저장하지 않습니다.

## 템플릿

재사용 가능한 템플릿은 `.claude/skills/adr/references/adr-template.md`에서 관리합니다.
