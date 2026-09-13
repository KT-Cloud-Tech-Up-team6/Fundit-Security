# SAST (정적 애플리케이션 보안 테스트)

SAST + 의존성 점검(SCA) 자동화 파이프라인입니다. 현재는 Fundit-backend를 주 대상으로 스캔하고 있으며, 이후 프론트엔드나 생성형AI 서비스, 외부 오픈소스, 컨테이너 이미지 점검 등으로 대상이 넓어질 수 있습니다.

## 도구

- **CodeQL** — `security-extended` 쿼리, `build-mode: autobuild`
- **Semgrep** — OWASP Top 10 / Java / 시큐리티 감사 / 시크릿 / JWT 공개 룰셋에 커스텀 룰을 더해서 사용 (`p/spring`은 레지스트리에 존재하지 않아 미사용)
- **OWASP Dependency-Check** — 의존성 취약점 점검(SCA), CVSS 등급까지 포함

## 폴더

- `rules/` — Semgrep 커스텀 룰이 들어갑니다
- `reports/` — 진단 보고서를 모아두는 곳입니다(SAST 진단서, 인증·암호화 정책 구현 검증 보고서 등 정제된 최종 문서만 커밋하고, 원시 스캔 출력은 커밋하지 않습니다 — `.gitignore` 참고)

## 실행 위치에 대해

워크플로는 이 레포(`Fundit-Security`)에서 돌고, `actions/checkout`으로 대상 레포지토리(현재는 Fundit-backend, `develop`)를 매번 읽기 전용으로 가져와 스캔합니다. 대상 레포지토리의 기존 워크플로나 브랜치 보호 규칙과는 별개로 독립적으로 동작하는 구조입니다. 향후 워크플로를 대상 레포지토리 쪽으로 직접 통합하는 것도 검토할 수 있습니다.
