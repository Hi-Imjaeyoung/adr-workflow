# Claude Code용 ADR 워크플로

Claude Code로 아키텍처 결정 기록(ADR, Architecture Decision Record)을 작성하고 검토하기 위한 가볍고 Git 친화적인 워크플로입니다.

> 상태: 스타터 템플릿 / 초기 프로토타입. 중요한 결정에 사용하기 전에 여러분의 저장소에서 워크플로를 먼저 검토하세요.

## 기능

- `/adr make <topic>` — ADR 초안을 만들고 문제를 정의합니다.
- `/adr options <ADR-ID>` — 가능한 대안과 트레이드오프를 비교합니다.
- `/adr review <ADR-ID>` — 가정, 근거, 완결성을 비판적으로 검토합니다.
- `/adr decide <ADR-ID>` — 사람이 승인한 결정과 그 결과를 기록합니다.
- `/adr list` — ADR 목록과 상태를 보여 줍니다.

이 워크플로는 **사실, 가정, 가설, 측정된 근거를 명확히 구분**하도록 설계되었습니다. Claude는 대안 분석을 도울 수 있지만, 최종 결정은 사람이 내립니다.

## 프로젝트에 설치하기

`.claude/`와 `docs/` 디렉터리를 프로젝트 루트에 복사합니다. 그런 다음 해당 저장소에서 Claude Code를 실행하고 다음을 입력합니다.

```text
/adr make content-storage-model
/adr options ADR-001
/adr review ADR-001
/adr decide ADR-001
/adr list
```

주제는 원하는 표현으로 적으면 됩니다. ID는 사용 가능한 다음 번호로 자동 부여됩니다.

## Plan Mode 관련 제약

Claude Code 스킬은 재사용 가능한 지침을 제공하고 슬래시 커맨드로 호출할 수 있지만, 스킬 자체가 대화형 세션의 권한 모드를 바꾼다고 가정해서는 안 됩니다. 실제로 읽기 전용인 계획 단계가 필요하다면 `/plan`(또는 사용 중인 버전의 해당 단축키)으로 Plan Mode에 들어간 뒤 `/adr make ...` 또는 `/adr options ...`를 실행하세요.

이 스킬은 Claude가 편집 전에 먼저 계획을 세우고, 최종 결정을 기록하기 전에 확인을 구하도록 지시합니다. 이는 보안 경계가 아니라 워크플로 가이드로 받아들이세요. 사용하는 Claude Code 버전에서 실제 동작을 확인하세요.

## 권장 저장소 구조

```text
.claude/
  skills/
    adr/
      SKILL.md
      references/
        adr-template.md
        decision-checklist.md
docs/
  adr/
    README.md
    000-template.md
```

## 상태 모델

- `Proposed` — 질문이 열려 있으며, 대안을 계속 검토할 수 있습니다.
- `Accepted` — 사람이 결정을 승인했습니다.
- `Rejected` — 이 대안/결정은 검토 후 기각되었습니다.
- `Superseded` — 이후의 ADR이 이 결정을 대체했습니다.
- `Deprecated` — 더 이상 적용되지 않는 결정입니다.

이력을 몰래 고쳐 쓰지 마세요. 결정이 바뀌면 새 ADR을 만들고 이전 기록과 연결합니다.

## Git 워크플로

1. 기능 브랜치에서 ADR을 작성/수정합니다.
2. 코드처럼 diff를 검토합니다.
3. 리뷰어에게 가정과 트레이드오프를 검증해 달라고 요청합니다.
4. 가능하면 관련 구현과 함께, 아니면 별도의 문서 커밋으로 ADR을 커밋합니다.
5. 결정이 바뀌면 새 ADR을 만들고 이전 ADR을 superseded로 표시합니다.

커밋 메시지 예시:

```text
docs(adr): record content storage decision
```

## 설계 원칙

1. 선호하는 해결책이 아니라 문제에서 출발합니다.
2. 의미가 있다면 최소 두 가지 실현 가능한 대안을 비교합니다.
3. 해당되는 경우 현상 유지(status quo)도 대안에 포함합니다.
4. 요구사항과 가정을 구분합니다.
5. 벤치마크나 예상 규모를 지어내지 않습니다.
6. 결과(consequences)와 재검토 조건을 명시합니다.
7. 결정을 `Accepted`로 바꾸기 전에 반드시 사람의 승인을 받습니다.
8. 크고 추측성인 문서보다 작고 유용한 ADR을 선호합니다.

## 라이선스

MIT. `LICENSE`를 참고하세요.
