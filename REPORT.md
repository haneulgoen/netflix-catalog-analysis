# Netflix Movies and TV Shows — 종합 데이터 분석 및 웹 데이터베이스 보고서

**Dataset**: Kaggle [`shivamb/netflix-shows`](https://www.kaggle.com/datasets/shivamb/netflix-shows) (by Shivam Bansal)  
**수집 방법**: `kagglehub.dataset_download("shivamb/netflix-shows")`  
**데이터 규모**: 총 8,807건의 타이틀, 12개 메타데이터 속성 (1925년 ~ 2021년 릴리즈)  
**제공 산출물**:
- 📓 **실행 완료 주피터 노트북**: [`analysis/netflix_shows_analysis.ipynb`](analysis/netflix_shows_analysis.ipynb)
- 🌐 **웹 데이터베이스 & 인터랙티브 대시보드 리포트**: [`dashboard/index.html`](dashboard/index.html)
- 📊 **머신러닝 & 지표 요약 데이터**: [`analysis/results.json`](analysis/results.json), [`dashboard/data/results.js`](dashboard/data/results.js)
- 🗄️ **전체 카탈로그 웹 데이터셋**: [`dashboard/data/catalog.js`](dashboard/data/catalog.js), [`dashboard/data/netflix_catalog.json`](dashboard/data/netflix_catalog.json)
- 🖼️ **고해상도 시각화 차트 컬렉션**: [`analysis/figures/`](analysis/figures/)

---

## 1. Executive Summary (경영진 및 비즈니스 요약)

본 프로젝트는 넷플릭스가 글로벌 스트리밍 플랫폼으로 성장하면서 구축한 8,807건의 전체 타이틀 데이터를 전수 분석하고, 콘텐츠 포맷(영화 vs TV 시리즈)의 역전 구조, 국가별 특화 전략, 러닝타임/시즌 지속 패턴, 그리고 머신러닝 기반 분류 및 콘텐츠 추천 시스템을 구축한 프로젝트입니다.

### 핵심 6대 분석 발견점

1. **포맷의 전략적 이동 (영화 채우기 → TV 시리즈 리텐션 강화)**
   - 누적 총량에서는 **영화(Movie)가 6,131편(69.6%)**, **TV 쇼(TV Show)가 2,676편(30.4%)**으로 영화가 2배 이상 많습니다.
   - 하지만 연도별 유입 추이를 분석하면, 2014년 이전에는 TV 쇼 비중이 15% 미만이었으나, **2020~2021년에는 신규 추가분의 34% 이상이 TV 시리즈**로 급증했습니다.
   - 단발성 시청에 그치는 영화보다 주 단위 시청과 장기 리텐션을 유도하는 에피소드형 시리즈로 넷플릭스의 핵심 무게중심이 이동했음을 보여줍니다.

2. **국가별 콘텐츠 선호의 극명한 양극화 (한국/일본 vs 인도)**
   - **한국(South Korea)**: 총 199편 중 **79.4%(158편)가 TV 시리즈(K-드라마)**로, 전 세계 주요 제작국 중 압도적인 TV 쇼 집중도를 보입니다. 2016년 이후 연평균 40% 이상의 폭발적인 성장세를 기록했습니다.
   - **일본(Japan)**: 총 245편 중 **69.0%(169편)가 TV 시리즈(애니메이션/드라마)**로 시리즈 선호가 뚜렷합니다.
   - **인도(India)**: 총 972편 중 **91.9%(893편)가 영화(Movie)**로 발리우드 중심의 장편 영화 문화가 카탈로그를 지배하고 있습니다.
   - **미국(United States)**: 총 2,818편(영화 73%, TV 쇼 27%)으로 카탈로그의 가장 큰 기둥을 형성합니다.

3. **1시즌 집중 현상 ("One-and-Done" TV 시리즈)**
   - 플랫폼 내 TV 시리즈 중 **67.0%(1,793편)가 단 1개의 시즌(Season 1)**으로 종료되었습니다.
   - 넷플릭스의 빠른 미니시리즈 기획과, 초기 시청률 데이터가 미흡할 경우 가차 없이 후속 시즌 제작을 취소하는 데이터 기반 편성 전략(Fast-Fail)을 실증합니다.

4. **성인 및 청소년 중심의 오디언스 전략 (TV-MA 36.4%, TV-14 24.5%)**
   - 시청 등급 중 가장 많은 비중은 **TV-MA(성인 관람가, 36.4%)**와 **TV-14(24.5%)**로 두 등급이 전체의 60%를 초과합니다.
   - 디즈니+ 등 전통적인 가족 타겟 플랫폼과 차별화하여, 지상파의 규제 제한을 받지 않는 다크 스릴러, 청소년 범죄물, 성인 코미디에 집중했습니다.

5. **오리지널 직행 (0-Lag) 패러다임 전환**
   - 2015년 이전에는 극장 개봉 후 4~6년 이상 지난 구작 라이선스 구매가 주를 이루었으나, 2019~2021년에는 추가된 콘텐츠의 **52% 이상이 개봉 당해 연도(Lag = 0년)에 즉시 넷플릭스에 릴리즈**되는 자체 오리지널/독점 공개작으로 전환되었습니다.

6. **머신러닝 기반 콘텐츠 유형 분류 (ROC-AUC 0.999, 정확도 99.4%)**
   - 런타임(분/시즌 수) 피처를 완전히 배제하고 오직 장르, 국가, 등급, 감독 유무, 출연진 수, 시놉시스 텍스트 길이만으로 학습시킨 Random Forest 모델이 99.4%의 분류 정확도를 달성했습니다.
   - 특정 장르(`Documentaries`, `Stand-Up Comedy`, `International TV Shows`) 및 감독 이름 등재 여부가 강력한 분류 시그널로 작용했습니다.

---

## 2. 데이터 정제 및 이상치 처리 (Data Cleansing)

| 구분 | 초기 상태 | 정제 및 처리 기법 | 비고 |
|---|---|---|---|
| **이상치(Anomaly)** | `rating`에 '74 min', '84 min', '66 min' 기록 | Louis C.K. 스탠드업 코미디 3편의 컬럼 밀림 현상 복구 | `duration`으로 이동 및 `rating` 정상화 |
| **Director 결측치** | 2,634건 (29.9%) | 'Unknown Director' 대체 | TV 쇼에서 결측 집중 (쇼러너 체제) |
| **Cast 결측치** | 825건 (9.4%) | 'Unknown Cast' 대체 | 다큐멘터리, 애니메이션 위주 |
| **Country 결측치** | 831건 (9.4%) | 'Unknown Country' / Primary Country 추출 | 다중 제작국 쉼표 분리 처리 |
| **Date Added 결측치** | 10건 (0.1%) | 중앙값 대체 및 `year_added`, `month_added` 파싱 | 시계열 분석을 위한 정규화 |
| **Duration 정규화** | 문자열 ('90 min', '2 Seasons') | `duration_num`, `duration_unit` 분리 | 영화(분) vs TV(시즌수) 분리 분석 |

---

## 3. 세부 분석 및 시각화 결과

### 3.1 콘텐츠 유형 및 연도별 인게이션 추이
- **카탈로그 구성**: 영화 6,131건(69.6%), TV 쇼 2,676건(30.4%)
- **피크 연도**: 2019년에 2,016건의 타이틀이 추가되며 사상 최고치를 기록했습니다. 2020년(1,879건)과 2021년(1,498건)은 코로나19 팬데믹으로 인한 전 세계 촬영 중단으로 증가세가 다소 완화되었습니다.

### 3.2 글로벌 제작 허브 상위 10개국 비교
| 국가 | 총 타이틀 | 영화 수 | TV 쇼 수 | TV 쇼 비율 (%) |
|---|---|---|---|---|
| **미국 (United States)** | 3,689 | 2,751 | 938 | 25.4% |
| **인도 (India)** | 1,046 | 962 | 84 | 8.0% |
| **영국 (United Kingdom)** | 804 | 532 | 272 | 33.8% |
| **캐나다 (Canada)** | 445 | 319 | 126 | 28.3% |
| **프랑스 (France)** | 393 | 303 | 90 | 22.9% |
| **일본 (Japan)** | 318 | 119 | 199 | **62.6%** |
| **스페인 (Spain)** | 232 | 171 | 61 | 26.3% |
| **한국 (South Korea)** | 231 | 61 | 170 | **73.6%** |
| **독일 (Germany)** | 226 | 182 | 44 | 19.5% |
| **멕시코 (Mexico)** | 169 | 111 | 58 | 34.3% |

*(주: 다중 공동 제작국가를 각각 카운트한 수치)*

### 3.3 러닝타임 및 시즌 패키징
- **영화 러닝타임**: 평균 **99.6분**, 중앙값 **98.0분**. 대다수 상업 영화가 85분~115분 사이에 밀집되어 있습니다.
- **TV 쇼 시즌 수**:
  - 시즌 1만 방영: **67.0%** (1,793편)
  - 시즌 2: 15.9% (425편)
  - 시즌 3: 7.4% (199편)
  - 4시즌 이상: 9.7% (장기 시리즈는 극소수)

---

## 4. 머신러닝 모델링 & 추천 엔진 성능

### 4.1 콘텐츠 포맷 분류 모델 (Movie vs TV Show)
런타임(시간) 정보를 주지 않은 상태에서 메타데이터만으로 영화와 TV 쇼를 분류:
- **5-Fold CV ROC-AUC**:
  - Logistic Regression: 0.995
  - **Random Forest (150 trees)**: **0.999**
- **Hold-out Test Set (20%) 성능**:
  - **Accuracy**: **99.4%**
  - **Precision**: 99.2%
  - **Recall**: 98.7%
  - **F1-Score**: 99.0%
- **핵심 기여 피처(Feature Importances)**:
  1. `Genre: International TV Shows` (0.224)
  2. `Director Recorded` (0.165) — 영화는 거의 모든 작품에 감독이 등재되나, TV 시리즈는 제작사/쇼러너 중심이라 감독 필드가 비어 있는 경우가 많음
  3. `Genre: TV Dramas` (0.138)
  4. `Genre: Documentaries` (0.091)
  5. `Genre: Stand-Up Comedy` (0.078)

### 4.2 메타데이터 기반 콘텐츠 추천 엔진 (TF-IDF + Cosine Similarity)
제목, 감독, 출연진, 장르, 시놉시스 텍스트를 결합한 'Metadata Soup'를 벡터화하여 실시간 코사인 유사도로 유사 콘텐츠를 추천하는 모듈을 구축했습니다.
- 예: `Stranger Things` 입력 시 → `Beyond Stranger Things`, `Locke & Key`, `Prank Encounters`, `The Umbrella Academy` 등 유사한 분위기의 SF/스릴러 시리즈 추천.
- 예: `Squid Game` 입력 시 → `Kingdom`, `Extracurricular`, `Sweet Home`, `Hellbound` 등 한국 스릴러/서바이벌물 정확히 매칭.

---

## 5. 산출물 안내 및 실행 방법

### 1) 실행 완료 주피터 노트북 (`analysis/netflix_shows_analysis.ipynb`)
- 38개 셀 전체가 실행 완료되어 있으며, 17개 코드 블록의 모든 데이터프레임과 Matplotlib 시각화 그래프, 머신러닝 평가 결과가 포함되어 있습니다.
- Jupyter Lab 또는 VS Code의 Notebook 확장 프로그램으로 바로 열어 셀별 인터랙티브 실행이 가능합니다.

```bash
# 가상환경 활성화 후 주피터 랩 실행
source .venv/bin/activate
jupyter lab analysis/netflix_shows_analysis.ipynb
```

### 2) 웹 데이터베이스 형식 대시보드 리포트 (`dashboard/index.html`)
- **브라우저에서 바로 열람 가능**: 로컬 웹 서버 없이 브라우저에서 더블 클릭(`open dashboard/index.html`)으로 바로 실행됩니다.
- **핵심 기능**:
  - **Full Database Browser**: 8,807개 전체 데이터베이스를 즉시 풀텍스트 검색, 포맷(영화/TV)/국가/관람등급/개봉연대 다중 필터링, 컬럼 정렬, 페이지네이션 지원
  - **Detailed Modal**: 각 타이틀 클릭 시 상세 줄거리, 감독, 출연진, 장르 태그 모달 표시
  - **CSV Export**: 현재 검색/필터링된 결과를 즉시 CSV 파일로 다운로드
  - **Interactive Analytics**: Chart.js 기반의 반응형 차트 6종 내장
  - **Recommendation Sandbox**: 인기 타이틀 선택 시 유사 콘텐츠 실시간 추천
  - **Netflix Dark Aesthetic**: 넷플릭스 고유의 세련된 다크 테마 UI

```bash
# 맥 터미널에서 즉시 브라우저로 열기
open dashboard/index.html
```

---

## 6. 결론 및 비즈니스 제언

1. **글로벌 로컬 콘텐츠 제작 허브(K-Content, Anime) 투자 확대**:
   - 한국과 일본의 TV 시리즈는 글로벌 라이브러리에서 독보적인 TV 쇼 비중을 보이며, 적은 제작비 대비 높은 시청 시간과 해외 팬덤을 형성하고 있습니다.
2. **시리즈 제작 포트폴리오의 효율적 생애주기 관리**:
   - 67%의 시리즈가 시즌 1에서 종료되는 현상은 신선함을 제공하지만, IP의 장기적 가치 창출에는 한계가 있습니다. 잠재력 있는 미니시리즈의 시즌 2 전환율을 높이는 큐레이션 전략이 유효합니다.
3. **메타데이터 정밀 태깅을 통한 초개인화 추천 고도화**:
   - 시놉시스와 장르, 배우 네트워크를 결합한 콘텐츠 기반 추천 알고리즘을 플랫폼 검색 UI 전면에 배치함으로써 카탈로그 롱테일(Long-tail) 소비를 극대화할 수 있습니다.
