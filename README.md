# karpathy-coding-principles-modified

> 이 레포는 [forrestchang/andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills)의 Karpathy 코딩 가이드라인 스킬(`karpathy-guidelines`)을 한국어로 옮기고 일부 수정한 버전입니다.
>
> - 원작자: Jiayuan Zhang ([@forrestchang](https://github.com/forrestchang))
> - 원작 라이선스: MIT
> - 원작의 바탕: [Andrej Karpathy의 LLM 코딩 함정 관찰](https://x.com/karpathy/status/2015883857489522876)

LLM이 코드 작업에서 자주 빠지는 함정(잘못된 가정, 과잉 복잡화, 무관한 영역 수정, 검증 불가능한 성공 기준)을 4원칙으로 막는 Claude 스킬입니다. 이 수정본은 여기에 "빌드·테스트를 돌릴 수 없는 환경에서는 정적 검증으로 대체한다"는 보강 원칙을 더했습니다.

## 원본과 달라진 점

| 구분 | 원본 | 이 수정본 |
| --- | --- | --- |
| 언어 | 영어 | 한국어 |
| 스킬 이름 | `karpathy-guidelines` | `karpathy-coding-principles-modified` |
| 구성 | 4원칙 본문 | 4원칙 본문 + 원본 README의 내용(문제 정의, 원칙별 표, Karpathy 인용, 작동 신호, 트레이드오프 노트)을 SKILL.md 안으로 가져옴. 원칙마다 「자기 점검 질문」을 붙이고 「적용 절차」 섹션을 둠 |
| 원칙 4-보강 | 없음 | 새로 추가 (아래) |
| 4원칙 표 | 4행 | `(보강) 빌드·테스트를 돌릴 수 없으면 정적 검증으로 대체한다` 행 추가 |
| 적용 절차 1단계 | 없음 | "빌드·테스트를 실제로 돌릴 수 있는 환경인지 판단하고, 불가하면 정적 검증으로 성공 기준을 세운다" 추가 |

추가한 「원칙 4-보강」의 내용 요약:

- 빌드 불가 환경의 신호를 정의한다: 외부 네트워크 차단, 의존성 캐시 부재, JDK 버전 불일치, `gradlew` CRLF 줄바꿈·빌드 래퍼 실행 불가.
- 착수 시 빌드 가능 여부를 먼저 판단하고, 불가하면 빌드를 시도하지 않는다.
- 대신 정적 검증으로 성공 기준을 세운다: 참조 심볼 존재, 시그니처 일치(Lombok 게터 포함), 호출부·예외 핸들러 연결, URL 패턴·정규식 매칭 대상 나열.
- 빌드를 못 돌린 사실과 로컬에서 확인할 수동 체크리스트를 결과에 명시한다.
- 빌드·테스트가 가능한 환경에서는 원본의 빌드·테스트 루프가 우선이다.

원칙 1~3과 원칙 4 본문의 취지는 원본과 같습니다.

## 왜 바꿨나

원본 원칙 4는 "테스트를 작성하고 통과시킨다"는 실행 검증을 전제로 합니다. 그런데 클라우드 샌드박스처럼 네트워크가 막혀 있거나 의존성 캐시가 없는 환경에서는 빌드 자체가 안 됩니다. 이때 AI가 빌드를 계속 재시도하며 시간을 쓰거나, 반대로 빌드를 못 돌렸는데도 검증 없이 "완료"라고 보고하는 일이 반복됐습니다.

원칙 4의 본질은 테스트 실행 자체가 아니라 "끝났는지 객관적으로 판정할 기준을 갖는 것"이라고 보고, 실행이 불가능할 때의 판정 기준을 정적 검증으로 명시했습니다.

## 언제 쓰나

- "이 버그 고쳐줘"
- "이 API에 검증 로직 추가해줘"
- "이 서비스 클래스 리팩토링해줘"
- 클라우드 환경에서 Java/Gradle 프로젝트 코드를 수정할 때처럼 빌드를 돌릴 수 없는 상황

사소한 오타 수정이나 명백한 한 줄 변경에는 전체 절차를 강제하지 않습니다(원본과 동일).

## 설치

Claude Code

```bash
mkdir -p ~/.claude/skills/karpathy-coding-principles-modified
curl -L https://raw.githubusercontent.com/smjae96/karpathy-coding-principles-modified/main/SKILL.md -o ~/.claude/skills/karpathy-coding-principles-modified/SKILL.md
```

Claude 앱(claude.ai): 이 레포 폴더를 zip으로 묶어 설정 > 기능 > 스킬에서 업로드

원본을 그대로 쓰고 싶다면 원작 레포의 설치 안내를 따르세요.

## 함께 쓰면 좋은 스킬

모음 레포: https://github.com/smjae96/claude-skills

## Attribution

- 원작: [andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills) by Jiayuan Zhang (@forrestchang), MIT License
- 원작의 원칙은 [Andrej Karpathy의 글](https://x.com/karpathy/status/2015883857489522876)에서 출발했습니다. 인용문의 출처도 같습니다.
- 수정: Jaeyun Shim (한국어 번역, 원칙 4-보강 추가, 표·적용 절차 보강, 이름 변경)
- 자세한 내용은 [NOTICE](./NOTICE)를 참고하세요.

## License

MIT. 원작 저작권 표기와 수정분 저작권 표기는 [LICENSE](./LICENSE)에 있습니다.

원작 레포는 README와 플러그인 메타데이터(`plugin.json`), SKILL.md 머리말에 MIT 라이선스를 명시하고 있지만 별도의 LICENSE 파일은 두고 있지 않습니다. 그래서 이 레포의 LICENSE는 표준 MIT 전문에 원작자 이름(원작 레포 커밋 기록 기준)을 적어 구성했습니다.
