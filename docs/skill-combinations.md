# 스킬 조합표

작업 상황별로 어느 묶음과 모듈을 어떤 순서로 쓰는지 정리한 표입니다.

- **굵은 글씨**는 이 저장소에 들어 있는 묶음 또는 모듈입니다. 모듈은 `묶음 › 모듈`로 적었습니다.
- `(별도 설치)`가 붙은 스킬은 이 저장소에 없습니다. 없으면 그 단계만 건너뛰면 되고, 나머지 흐름은 그대로 돌아갑니다.
- 국문 원고에는 어떤 조합이든 문체 기준과 점검 단계를 끼워 넣습니다. 제안서·보고서는 개조식/서술식을 먼저 정합니다. 논문은 `mechanical-pen-academic`, 기획서·보고서는 `mechanical-pen-proposal`의 `check_style.py`로 경고 3개 이하를 맞춘 뒤 다시쓰기를 별도 단계로 합니다.

## 학술 논문

| 상황 | 순서 | 비고 |
|---|---|---|
| 섹션 초안(서론·방법·실험·결론) | **academic › research-paper-writing** → **mechanical-pen-academic**(국문 문체 기준) | 구조와 문단 흐름은 모듈, 문장은 묶음 기준 |
| 초록 | **academic › research-paper-writing**(초록 틀) → **mechanical-pen-academic** | |
| 문장 다듬기 | **academic › cs-academic-writing** → LaTeX 원고면 **academic › latex-rhythm-refiner** | 인용·수치·주장 범위는 바꾸지 않음 |
| 국문 원고 문체 점검 | **mechanical-pen-academic** `check_style.py --register paper` → 경고 3개 이하 → 별도 다시쓰기 | 고친 문장은 "전 → 후" 표로 보고 |
| 투고 전 교정·검토 | **academic › claude-code-paper-writing**(먼저 문제 목록만) → 승인 후 수정 | 인용 실존 확인은 **mechanical-pen-academic**의 `references/citation_verification.md` |
| 가상 심사(내 논문) | **academic › claude-code-paper-writing**(reviewer simulation) | |
| 연구 계획·결론 사전 반론 | **proposal › the-fool**(pre-mortem, red team, 근거 감사) | |
| 학위논문 계획서·연구계획서 | **academic › research-proposal** → **mechanical-pen-academic** | 한국어면 영어 골격을 따르되 국문 학술 문체 |
| 리뷰(서베이) 논문 전체 | **academic › arxiv-paper-writer** | 실험 논문에는 쓰지 않음 |
| 기술 블로그·해설 글 | **academic › karpathy-article-writing** | 그 문체를 원할 때만 |
| 문헌 조사·인용 관리 | `literature-review`, `citation-management`(별도 설치) → **mechanical-pen-academic** 인용 검증 | |

## 발표

| 상황 | 순서 | 비고 |
|---|---|---|
| 학회 발표·세미나·학위 심사 슬라이드 | **academic › academic-pptx**(논증 구조, 핵심 문장 제목, `korean_conference_guide.md`) → `pptx`(별도 설치, 파일 생성) → 그림은 **mechanical-pen-figures** | 10장 넘으면 목차부터 확인 |
| 발표 대본·리허설·예상 질문 | **academic › academic-pptx**의 `script_and_qa.md` → 대본은 슬라이드 노트에 | 수치를 지어내지 않음 |

## 기획서·제안서·보고서

| 상황 | 순서 | 비고 |
|---|---|---|
| 공모전 기획서·사업계획서 | **mechanical-pen-proposal**(먼저 개조식/서술식 확인 → 배점별 목차, 스토리텔링, 운영 설계, 형식별 문체 기준) → 사례 조사 `deep-research`(별도 설치) → 사전 반론 **proposal › the-fool** → 모식도 **mechanical-pen-figures** → 그래프 **figures › sci-figure** → 한글 양식 **proposal › hwpx-editing** | 개조식은 `--register proposal`, 서술식은 `--register proposal_narrative`로 경고 3개 이하 |
| 연구비·과제 제안서 | `research-grants`(별도 설치, 내용 구성) → **mechanical-pen-proposal**(문장 기준, 인용 검증) | 기관 양식의 예산표·서식은 채우지 않음 |
| 연구보고서·연차보고서·요약문 | **mechanical-pen-proposal** `check_style.py --register report\|summary`(서술식 보고서는 `report_narrative`) → 별도 다시쓰기 | |
| 운영형 시스템(경보·예측·의사결정 지원) 제안 | **mechanical-pen-proposal**의 `references/operational_design_checklist.md` | 가동 조건, 경보 규칙, 해제 시점, 오경보 비용, 과거 사례 연계 |
| 한글(.hwpx) 읽기·편집·표 추출·복구 | **proposal › hwpx-editing** | 원본은 두고 사본에서 작업 |
| 옛 .hwp 변환, Word → 한글 조판 | **proposal › hwpx-editing** → **mechanical-pen-proposal** `scripts/docx2hwpx.py`, `merge_hwpx.py` | Windows 한글 프로그램과 `pywin32` 필요. 실행 전 열린 한글 문서를 저장하고 닫기 |

## 그림

| 상황 | 순서 | 비고 |
|---|---|---|
| 연구 흐름도·모식도·구조도·서비스 구성도·추진 체계도·그래픽 초록 | **mechanical-pen-figures**(`references/rs-workflow-style.md` §7·§8 문법, §9 분포 기준) → `check_figure.py` 경고 0개, 글자 겹침 0개 | 참조 구현 `examples/architecture_reference.py` |
| 투고용 데이터 그래프(막대·선·산점·히트맵·다중 패널) | **figures › sci-figure** → 보조 **figures › scientific-visualization** | 한글 라벨이면 맑은 고딕 |
| 보고서·발표용 그림, 색·대비·접근성 감사 | **figures › scientific-visualization** | |
| 색상표 선택(순차·발산·범주형, 색각 이상 대응) | **figures › colormaps-styling** | |
| 논문용 지도 | `cartography-geoviz`(별도 설치) → 색상표는 **figures › colormaps-styling** | |
