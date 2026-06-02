# 상장 제조기 (autocertpage)

브라우저만으로 동작하는 **단일 HTML 상장(Certificate) 제작 도구**입니다. 설치·서버 없이 `index.html`을 열어 바로 사용합니다. 입력 내용·설정은 브라우저 `localStorage`에 자동 저장됩니다.

## 주요 기능
- **여러 페이지 작업**: 페이지 N장 일괄 복제, 삭제, 페이지별 독립 내용(수상자·도장)
- **CSV 일괄 생성**: 명단 CSV 업로드(업로드 시 *전체 교체 / 기존에 추가* 선택), 작성용 **예시 CSV 다운로드** 제공
- **칸 클릭 인라인 인스펙터**: 텍스트 칸을 클릭하면 그 칸 전용으로 **글자 크기 · 자간 · 정렬(좌/중/우)** 조절
- **전역 조절 패널(접이식)**: 레이아웃 간격 / 이중 외곽선(굵기·색·가장자리 여백·두 선 사이 간격) / 로고 교체·높이 / **영문 폰트 선택** / **가로↔세로** 방향 토글
- **도장**: 이미지 드래그·업로드, 위치 드래그 이동, 크기 조절
- **로고**: 원하는 회사 로고 이미지 업로드(기본은 중립 플레이스홀더)
- **PDF 저장**: 브라우저 인쇄(→PDF). 다중 페이지는 한 장씩 분리 출력

## 사용법
1. `index.html`을 브라우저에서 연다
2. 텍스트를 **클릭**해 편집 (클릭 시 크기·자간·정렬 미니패널이 뜸)
3. 우측 상단 툴바: 페이지 **복제 추가 / 삭제**, **CSV 불러오기 / 예시 CSV**, **조절** 패널, **잠금**, **초기화**
4. **PDF로 저장** 버튼 → 인쇄 대화상자에서 PDF로 저장

## CSV 형식
헤더(영문 키, 순서·부분 지정 가능):

```
issue,title,tag,name,aff,body,date,org,role,signer
```

- 한 행 = 상장 1장. 지정하지 않은 열은 기본값을 사용합니다.
- 쉼표·따옴표·줄바꿈이 포함된 값은 큰따옴표로 감싸 처리됩니다(RFC 4180 호환).
- 인식 못 하는 열은 무시됩니다. 툴바 **예시 CSV**로 양식을 받으세요.

## 적용 범위
- **모든 페이지 공통**: 외곽선 · 로고 · 방향 · 간격 · 글자 크기 · 자간 · 정렬 · 영문 폰트
- **페이지별 독립**: 텍스트 내용, 도장 이미지·위치

## 폰트
영문/숫자 표기(상장번호, `Certificate of Excellence` 부제, 발급기관명 등)에 사용되는 폰트를 **조절 패널 → 페이지 · 브랜드 → 영문 폰트**에서 토글로 선택할 수 있습니다(선택 결과는 자동 저장).

| 옵션 | 필요한 파일 | 비고 |
| --- | --- | --- |
| **Pretendard SemiBold** (기본) | `fonts/Pretendard-SemiBold.woff2` | 무료 / OFL. 권장 |
| **GT Planar** | `fonts/GT-Planar-Regular.woff2`, `fonts/GT-Planar-Medium.woff2` | **유료 라이선스 필요** — 별도 구매 후 직접 배치 |

한글 본문은 모든 옵션에서 Pretendard(Regular/Medium/SemiBold/Bold)를 사용합니다. `fonts/Pretendard-Regular.woff2`, `Pretendard-Medium.woff2`, `Pretendard-Bold.woff2`도 함께 넣어두면 좋습니다.

폰트 파일이 없으면 Pretendard 다른 weight → 시스템 폰트(`-apple-system`, `BlinkMacSystemFont`, `Malgun Gothic` 등) 순으로 자동 폴백되므로 **폰트 없이도 동작**합니다.

> 참고: GT Planar는 Grilli Type의 상용 폰트입니다. 라이선스 미보유 시 기본값(Pretendard SemiBold)을 그대로 사용하세요.

## 기술 메모
- 의존성 없음(바닐라 JS). CSS 커스텀 프로퍼티로 전역 설정 제어.
- 영문 폰트는 `--ff-en` (font-family) + `--fw-en` (font-weight) 두 CSS 변수로 스위칭. 선택값은 `cert-settings.enFont`에 저장.
- 저장 키: `cert-pages`, `cert-settings`. 구버전 키(`aim-cert-*`)가 있으면 최초 로드 시 자동 이관.

## 라이선스
미정.
