# SAST 진단 보고서 (요약)

- 대상: `Fundit-backend` (`develop`)
- 도구: CodeQL (`security-extended` 쿼리), Semgrep (`p/owasp-top-ten` `p/java` `p/security-audit` `p/secrets` `p/jwt` + 커스텀 룰 4종), OWASP Dependency-Check
- 최근 갱신: 2026-09-18 (내용 기준 2026-09-15 트리아지, 9/16·9/17 재스캔에서 신규 발견 없음을 확인해 그대로 유지)
- **이 문서는 요약본입니다.** 정확한 파일·라인·트리거 조건 등 상세 내용은 별도 비공개 채널(보안팀 관리 문서)로 전달되며, 이 public 레포에는 커밋하지 않습니다. 상세 내용이 필요하면 보안팀에 문의 바랍니다.
- 분류 기준: 
(1) **조치 필요** — 확정된 문제 및 위협
(2) **판단 보류** — 위험 여부를 코드 검토만으로 확정하지 못한 항목 
(3) **조건부 위험** — 라이브러리·버전 자체는 실제로 유효한 CVE 대상이지만, 그 취약한 기능을 현재 쓰지 않아 지금 당장은 위험하지 않은 항목(설정 변경 시 재확인 필요) 
(4) **오탐으로 판단해 제외함**
- **알려진 커버리지 한계**: 최근 추가된 신규 서비스 하나가 빌드 설정에 아직 등록되지 않아, 빌드 기반 도구(CodeQL autobuild, Dependency-Check)가 검사 대상에 포함하지 못하고 있습니다. Semgrep은 파일 단위 스캔이라 다음 실행부터 반영될 예정입니다.

## 요약 표

| # | 분류 | 심각도 | 발견 도구 |
|---|---|---|---|
| 1 | 조치 필요 | Critical | Dependency-Check |
| 2 | 조치 필요 | High | CodeQL |
| 3 | 조치 필요 | Medium | CodeQL |
| 4 | 조치 필요 | Medium | CodeQL |
| 5 | 판단 보류 | Medium | Dependency-Check |
| 6 | 조건부 위험 | Critical | Dependency-Check |
| 7 | 조건부 위험 | High | Dependency-Check |
| 8 | 조건부 위험 | High | Dependency-Check |
| 9 | 조건부 위험 | Medium | Dependency-Check |
| 10 | 조건부 위험 | High | Dependency-Check |
| 11 | 조건부 위험 | High | Dependency-Check |
| 12 | 참고/보강 권고 | Low | CodeQL |
| 13 | 참고/보강 권고 | - | Semgrep |
| - | 오탐 제외 | - | CodeQL |
| - | 오탐 제외 | - | Dependency-Check |
| - | 오탐 제외 | - | Dependency-Check |
| - | 오탐 제외 | - | Dependency-Check |

## 집계

- 조치 필요: Critical 1건, High 1건, Medium 2건 (총 4건)
- 판단 보류: 1건
- 조건부 위험: 6개 항목(개별 CVE 기준 10건)
- 참고/보강 권고: 2건
- 오탐으로 판단해 제외: 4개 그룹

## 도구/아키텍처 관련 메모

- 이 스캔은 `Fundit-Security` 레포에서 `Fundit-backend`를 외부 checkout으로 가져와 실행한 것입니다.
- Dependency-Check는 매주(CodeQL·Semgrep은 매일) 재스캔되며, 다음 스캔 결과가 나오면 이 요약도 함께 갱신합니다.
