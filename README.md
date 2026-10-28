# Google Trends로 살펴본 한국 마라탕 유행의 확산과 재유행 요인: 2019·2022·2024년 정점 비교

Google Trends의 "마라탕" 월별 검색 관심도(한국, 2016-01 ~ 2026-09)를 분석한 프로젝트입니다. 세 가지를 봤습니다. **언제 관심이 오르기 시작했는지**, **2019·2022·2024년 세 번 비슷한 수준으로 찍은 최상위 관심도가 각각 왜 생겼고 얼마나 유지됐는지**, **계절에 따른 차이가 있는지, 관심이 꾸준히 유지되는지**.

분석 결과와 해석은 [REPORT.md](REPORT.md)에 정리되어 있습니다.

## 폴더 구조

```
maratang-trend-analysis/
|-- data/
|   |-- maratang_kr_raw.csv        # Google Trends 원본 (2015-12 ~ 2026-09, 130개월)
|-- images/
|   |-- 01_trend_moving_average.png  # 전체 추세 + 12개월 이동평균
|   |-- 02_yoy_change.png            # 전년 동월 대비 변화율
|   |-- 03_peak_duration.png         # 지수 80 이상 고점 구간과 지속 기간
|   |-- 04_seasonality.png           # 연도별 계절 차이 (추세 제거 값)
|   |-- 05_stl_decomposition.png     # STL 분해 (추세/계절성/잔차)
|   |-- 06_peak_comparison.png       # 세 정점(2019·2022·2024) 정렬 비교와 기준별 지속 기간
|-- analysis.ipynb                 # 전체 분석 코드
|-- REPORT.md                      # 분석 리포트
|-- requirements.txt
|-- README.md
```

## 실행 방법

Python 3.11 이상이 필요합니다 (작성 환경: Python 3.11.15, Windows 11).

```bash
# 1. 가상환경 생성 및 활성화
python -m venv .venv
.venv\Scripts\activate          # Windows
# source .venv/bin/activate     # macOS / Linux

# 2. 의존성 설치
pip install -r requirements.txt

# 3-a. 노트북을 열어 위에서부터 순서대로 실행
jupyter notebook analysis.ipynb

# 3-b. 또는 한 번에 실행
jupyter nbconvert --to notebook --execute --inplace analysis.ipynb   # images/ 의 그래프 6개가 다시 생성됨
```

> 그래프의 한글 표시를 위해 `Malgun Gothic`(Windows 기본 폰트)을 사용합니다. macOS는 `AppleGothic`, Linux는 `NanumGothic` 등으로 노트북 첫 코드 셀의 `font.family`를 바꿔 주세요.

## 데이터

| 항목 | 내용 |
|---|---|
| 출처 | [Google Trends](https://trends.google.com/trends/) |
| 검색어 | 마라탕 (검색어) |
| 지역 / 단위 | 대한민국 / 월별 |
| 원본 기간 | 2015-12 ~ 2026-09 (130개월) |
| 분석 기간 | 2016-01 ~ 2026-09 (129개월) |
| 값의 의미 | 검색 횟수가 아니라, 조회 기간 중 최고점을 100으로 둔 **상대 관심도 지수(0~100)** |

### 수집 방법 (재현)

1. https://trends.google.com/trends/ 접속
2. 검색어 `마라탕` 입력, 지역 `대한민국`, 기간을 2015-12 ~ 2026-09가 포함되도록 설정
3. "시간 흐름에 따른 관심도" 차트의 다운로드(CSV) 버튼 클릭
4. 상단 안내 행을 지우고 `Time`, `마라탕` 두 컬럼만 남겨 `data/maratang_kr_raw.csv`로 저장

- 다운로드 일자: 2026-10-28

### 주의 사항

- Google Trends 지수는 표본 기반으로 계산되고 조회 기간에 따라 다시 정규화되므로, **같은 조건으로 다시 내려받아도 값이 조금 다를 수 있습니다.** 재현할 때는 저장소에 포함된 CSV를 사용하세요.
- 데이터 저작권은 Google에 있습니다. 이 저장소는 학습 목적으로 원본 CSV를 포함하며, 인용 시 출처를 "Google Trends (https://trends.google.com)" 로 표기합니다. 상업적으로 쓰려면 Google 서비스 약관을 확인하세요.
