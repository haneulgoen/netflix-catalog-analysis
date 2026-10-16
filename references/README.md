# Reference Management & Citation Guide

이 폴더는 프로젝트에서 사용된 데이터셋, 학술 논문, 비즈니스 리포트, 기사 등의 레퍼런스를 체계적으로 관리하고, 슬라이드덱 및 보고서에서 손쉽게 인용할 수 있도록 구성되어 있습니다.

---

## 📁 폴더 내 파일 구성

```
references/
├── README.md             # 본 가이드 문서 (레퍼런스 관리 방법 및 인용 규칙)
├── sources.json          # 구조화된 참고문헌 데이터베이스 (슬라이드덱 연동)
└── data_dictionary.md    # 넷플릭스 데이터셋 컬럼 정의 및 정제 규칙
```

---

## ✍️ 새 레퍼런스 추가 방법

새로운 논문, 기사, 보고서를 추가하려면 `references/sources.json` 파일의 `"references"` 배열에 아래 형식으로 객체를 추가하세요.

```json
{
  "id": "REF-07",
  "category": "Industry Report / Academic Paper / News / Dataset",
  "title": "참고 문헌 또는 보고서 제목",
  "author": "저자 또는 발행 기관명",
  "year": 2024,
  "source": "발행처 (예: Nature, HBR, Wall Street Journal, Kaggle 등)",
  "url": "https://링크주소.com",
  "citation": "저자. (연도). 제목. 발행처.",
  "note": "이 레퍼런스가 본 분석의 어떤 부분(예: K-드라마 성장률, 추천 알고리즘)과 연결되는지 한 줄 요약"
}
```

---

## 🎯 슬라이드덱 및 보고서 인용 규칙

### 1) HTML 슬라이드덱 (`slides/index.html`)에서 인용할 때
슬라이드 하단의 각주 또는 뱃지로 레퍼런스 ID와 원문 링크를 표기합니다:

```html
<!-- 슬라이드 하단 레퍼런스 뱃지 예시 -->
<div class="slide-citation">
  <span class="cite-tag">REF-01</span> Kaggle: shivamb/netflix-shows
  <span class="cite-divider">·</span>
  <span class="cite-tag">REF-02</span> Netflix Q3 2021 Shareholder Letter
</div>
```

### 2) 마크다운 보고서 (`REPORT.md`)에서 인용할 때
본문 내에 `[REF-01]` 형식으로 각주 링크를 달아줍니다:

```markdown
넷플릭스의 비영어권 로컬 콘텐츠 투자 확대는 주주서한에서도 핵심 전략으로 강조되었습니다 [REF-02](references/sources.json).
```

---

## 📚 주요 카테고리별 레퍼런스 가이드

1. **데이터셋 (Dataset)**: Kaggle, 데이터 저장소의 버전 정보 및 원저작자 표기.
2. **산업/투자 보고서 (Industry Report)**: 넷플릭스 주주서한, SEC 10-K 공시, 스트리밍 산업 전문 분석 리포트.
3. **학술 논문 (Academic Paper)**: 추천 시스템 알고리즘 (TMIS), 시청률 예측 및 콘텐츠 수명 주기 논문.
4. **비즈니스 기사 (Business Case)**: Variety, Deadline, HBR 등의 시즌 캔슬 정책, 제작비 단가 분석 기사.
