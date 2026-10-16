# 🎬 Netflix Catalog Intelligence & Web Platform

> Kaggle의 `shivamb/netflix-shows` 데이터셋(8,807건)을 기반으로 한 **종합 데이터 분석**, **실행 주피터 노트북**, **인터랙티브 웹 데이터베이스**, **HTML 슬라이드덱**, 그리고 **체계적인 레퍼런스 관리 시스템**을 갖춘 프로젝트입니다.

🌐 **GitHub Pages 라이브 배포 URL**:
- 🎯 **HTML 슬라이드덱**: [https://haneulgoen.github.io/netflix-catalog-analysis/](https://haneulgoen.github.io/netflix-catalog-analysis/)
- 🗄️ **웹 데이터베이스 뷰어**: [https://haneulgoen.github.io/netflix-catalog-analysis/dashboard/index.html](https://haneulgoen.github.io/netflix-catalog-analysis/dashboard/index.html)
- 📦 **GitHub 저장소**: [https://github.com/haneulgoen/netflix-catalog-analysis](https://github.com/haneulgoen/netflix-catalog-analysis)

---

## 📂 프로젝트 전체 폴더 맵 (Project Structure)

프로젝트는 용도별로 명확하게 4개 서브시스템으로 구분되어 있어 쉽게 탐색하고 확장할 수 있습니다.

```
netflix-catalog-analysis/
├── README.md                      # [현재 파일] 전체 프로젝트 개요 및 폴더 안내 가이드
├── REPORT.md                      # 경영진/비즈니스용 심층 마크다운 분석 보고서
├── requirements.txt               # 프로젝트 파이썬 의존성 패키지 목록
│
├── 🎯 slides/                     # [프레젠테이션] 반응형 HTML 슬라이드덱
│   ├── index.html                 # 키보드(←, →, F, R) 조작 지원 프레젠테이션 슬라이드 (12장)
│   └── README.md                  # 슬라이드덱 조작법 및 커스터마이징 가이드
│
├── 📚 references/                 # [참고문헌] 데이터 사전 및 학술/비즈니스 레퍼런스
│   ├── README.md                  # 레퍼런스 추가 방법 및 슬라이드/보고서 인용 규칙
│   ├── sources.json               # 구조화된 참고문헌 DB (Kaggle, ACM 논문, 주주서한 등)
│   └── data_dictionary.md         # 데이터셋 12개 컬럼 명세 및 정제 규칙
│
├── 📓 analysis/                   # [데이터 분석 & 모델링] 주피터 노트북 및 시각화
│   ├── netflix_shows_analysis.ipynb # 38개 셀 전체 실행 완료된 분석 노트북 원본
│   ├── build_notebook.py          # 노트북 빌드 및 자동 실행 파이프라인
│   ├── results.json               # 머신러닝 성능 및 지표 요약 데이터
│   ├── data/
│   │   └── netflix_titles.csv     # 8,807건 넷플릭스 원본 데이터
│   └── figures/                   # 고해상도 시각화 차트 이미지 컬렉션 (01~11)
│
└── 🌐 dashboard/                  # [웹 데이터베이스] 브라우저 기반 풀 카탈로그 뷰어
    ├── index.html                 # 8,807개 전체 타이틀 실시간 검색·필터·모달·CSV 내보내기 웹앱
    └── data/
        ├── catalog.js             # 무설치 로컬 실행을 위한 Zero-CORS 카탈로그 데이터
        ├── netflix_catalog.json   # JSON 형식 전체 카탈로그
        └── results.js             # 대시보드 통계 및 Chart.js 시각화용 데이터
```

---

## ⚡ 빠른 실행 명령어 (Quick Start)

### 1. 발표용 슬라이드덱 열기
```bash
open slides/index.html
```
- <kbd>→</kbd> / <kbd>Space</kbd>: 다음 슬라이드
- <kbd>F</kbd>: 전체화면 모드
- <kbd>R</kbd>: 우측 레퍼런스(참고문헌) 서랍 토글
- <kbd>O</kbd>: 전체 슬라이드 썸네일 개요 보기

### 2. 전체 카탈로그 웹 데이터베이스 열기
```bash
open dashboard/index.html
```
- 8,807건 전체 타이틀에 대한 즉시 검색, 다중 필터(영화/TV, 국가, 등급, 연대), 상세 모달, CSV 내보내기 제공

### 3. 데이터 분석 주피터 노트북 실행하기
```bash
source .venv/bin/activate
jupyter lab analysis/netflix_shows_analysis.ipynb
```

---

## 📚 레퍼런스 관리 시스템 (`references/`)

본 프로젝트는 분석 수치와 주장의 신뢰성을 뒷받침하기 위해 공식 출처를 체계적으로 분리 관리합니다.

| 식별자 | 카테고리 | 제목 | 출처 | 주요 연결 분석 내용 |
|---|---|---|---|---|
| **REF-01** | Dataset | Netflix Movies and TV Shows | Kaggle (Shivam Bansal) | 8,807건 전수 데이터 스키마 및 등급 분포 |
| **REF-02** | Report | Q3 2021 Letter to Shareholders | Netflix, Inc. | 한국(K-드라마) 등 비영어권 로컬 콘텐츠 글로벌 전략 |
| **REF-03** | Paper | The Netflix Recommender System | ACM TMIS (Gomez-Uribe & Hunt) | 개인화 추천 알고리즘 및 가입자 이탈 방지(Anti-Churn) |
| **REF-04** | Business | The 'One Season' Cancellation Model | Variety VIP (A. Wallenstein) | TV 시리즈 67%가 시즌 1에서 종료되는 경제적 원인 |
| **REF-05** | Tech Spec | Scikit-learn: Machine Learning in Python | JMLR (Pedregosa et al.) | Random Forest (AUC 0.999) 및 TF-IDF 벡터화 |
| **REF-06** | Code | Executed Jupyter Analysis Notebook | Workspace | 전수 실행된 38개 셀 주피터 분석 원본 |

- 새 레퍼런스를 추가하는 방법은 [`references/README.md`](references/README.md)를 참고하세요.

---

## 📊 5대 핵심 분석 발견점

1. **포맷의 역전**: 누적 카탈로그는 영화(69.6%)가 우세하나, 2020~2021년 신규 등록분의 **34% 이상이 TV 시리즈**로 급증하여 리텐션 중심 플랫폼으로 진화.
2. **K-콘텐츠의 극단적 시리즈 집중**: 한국 타이틀 199편 중 **79.4%가 TV 시리즈(K-드라마)**로 글로벌 최고 수준 (인도의 영화 91.9% 비중과 극명한 대조).
3. **1시즌 캔슬 패러독스**: TV 쇼의 **67.0%가 단 1개의 시즌**으로 종료 (제작비 상승 곡선 대비 신규 가입 기여도 체감에 따른 Fast-Fail 편성).
4. **성인 지향적 라인업**: **TV-MA(36.4%) + TV-14(24.5%) = 60.9%**로 지상파 규제를 탈피한 성인 스릴러·다큐멘터리 집중.
5. **머신러닝 포맷 예측**: 런타임을 배제하고 장르, 감독 기록 유무 등 메타데이터만으로 **Random Forest 분류기 정확도 99.4% (ROC-AUC 0.999)** 달성.
