# Netflix Dataset — Data Dictionary & Cleansing Spec

Kaggle `shivamb/netflix-shows` 데이터셋의 컬럼 정의 및 전처리 규칙입니다.

---

## 1. Raw Dataset Schema (8,807 rows × 12 columns)

| 컬럼명 | 원본 타입 | 결측치 수 (비율) | 설명 | 예시 |
|---|---|---|---|---|
| `show_id` | string | 0 (0%) | 고유 콘텐츠 식별자 (Unique ID) | `s1`, `s2` |
| `type` | string | 0 (0%) | 콘텐츠 포맷 (`Movie` 또는 `TV Show`) | `Movie`, `TV Show` |
| `title` | string | 0 (0%) | 콘텐츠 공식 제목 | `Stranger Things` |
| `director` | string | 2,634 (29.9%) | 감독 이름 (TV 쇼는 결측치 다수) | `Kirsten Johnson` |
| `cast` | string | 825 (9.4%) | 주요 출연진 목록 (쉼표 구분) | `Winona Ryder, David Harbour` |
| `country` | string | 831 (9.4%) | 제작 또는 공동 제작 국가 (쉼표 구분) | `United States, South Korea` |
| `date_added` | string | 10 (0.1%) | 넷플릭스 플랫폼 등록 일자 | `September 25, 2021` |
| `release_year` | integer | 0 (0%) | 콘텐츠의 최초 개봉/방영 연도 | `2016`, `2021` |
| `rating` | string | 4 (0.05%) | 시청 연령 등급 (TV-MA, PG-13 등) | `TV-MA`, `TV-14` |
| `duration` | string | 3 (0.03%) | 영화: 러닝타임(분) / TV: 시즌 수 | `90 min`, `2 Seasons` |
| `listed_in` | string | 0 (0%) | 배정된 장르 카테고리 (쉼표 구분) | `Dramas, International Movies` |
| `description` | string | 0 (0%) | 줄거리 시놉시스 (텍스트 요약) | `As her father nears the end...` |

---

## 2. 이상치(Anomaly) 처리 내역

### Louis C.K. 스탠드업 코미디 3편의 컬럼 밀림
- **대상 레코드**:
  - `s5542` (Louis C.K. 2017)
  - `s5795` (Louis C.K.: Hilarious)
  - `s5814` (Louis C.K.: Live at the Comedy Store)
- **증상**: 원본에서 `duration`이 결측(NaN)이고, `rating` 컬럼에 러닝타임(`74 min`, `84 min`, `66 min`)이 잘못 기록됨.
- **처리**:
  ```python
  mask = df["duration"].isnull() & df["rating"].str.contains("min", na=False)
  df.loc[mask, "duration"] = df.loc[mask, "rating"]
  df.loc[mask, "rating"] = np.nan  # 또는 'Unknown'
```

---

## 3. 엔지니어링된 파생 컬럼 (Engineered Features)

| 파생 변수명 | 데이터 타입 | 생성 로직 및 산출 방식 | 분석 목적 |
|---|---|---|---|
| `year_added` | int / float | `pd.to_datetime(df['date_added']).dt.year` | 연도별 카탈로그 신규 유입 추이 파악 |
| `month_added` | int / float | `pd.to_datetime(df['date_added']).dt.month` | 콘텐츠 등록 월별 계절성(Seasonality) 분석 |
| `addition_lag_years` | int / float | `year_added - release_year` | 개봉 후 넷플릭스 등록까지의 시차 (0이면 오리지널 직행) |
| `duration_num` | float | `duration` 문자열에서 숫자 추출 | 영화 평균 러닝타임 및 TV 시즌 수 정량 분석 |
| `duration_unit` | string | `duration`에서 `min` 또는 `Season(s)` 분리 | 영화/TV 포맷 단위 구분 |
| `target_audience` | category | 등급 그룹화: `Kids`, `Teens`, `Adults`, `Other` | 시청 타겟층 인구통계학적 세그멘테이션 |
| `primary_country` | string | `country`에서 첫 번째 국가 추출 | 대표 제작국 기준 집계 |
| `metadata_soup` | text | 제목 + 감독 + 출연진 + 장르 + 시놉시스 결합 | TF-IDF 코사인 유사도 추천 엔진 임베딩 |
