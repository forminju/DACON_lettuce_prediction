# 상추의 생육 환경 생성 AI 경진대회
![대회설명이미지](https://user-images.githubusercontent.com/92534659/209780762-7153a789-b52a-41a9-a108-11a351c41bef.png)

## 대회 개요
- 주최: KIST 강릉분원
- 주관: [데이콘](https://dacon.io/competitions/official/236033/overview/description)
- 기간: 2022.11.21 ~ 2022.12.19
- 주제: 생육 환경 생성 AI 모델 결과를 바탕으로 상추의 일별 최대 잎 중량을 도출할 수 있는 최적의 생육 환경 조성

## 목표
1. 상추의 일별 잎중량을 예측하는 AI 예측 모델 개발 (정량평가)
2. 예측 모델을 활용하여 생육 환경 생성 AI 모델 개발 (정성평가)

&rarr; 생성 AI 모델 결과로부터 상추의 일별 최대 잎 중량을 도출할 수 있는 최적의 생육 환경 조성 및 제안 (최종 결과물)

## 결과
- **최종 4위 / 137팀 (상위 3%)**
- Public Score 8위 4.79935 | Private Score 6위 8.55621
- 최종 순위는 정성평가 포함한 결과

## DataSet
[출처](https://dacon.io/competitions/official/236033/data)

Input
  - DAT : 생육 일 (0~27일차)
  - obs_time : 측정 시간 (1시간 간격)
  - 상추 케이스 별 환경 변수 15개 : 온도, 습도, co2, ec, 분무량, 광량 등 (1시간 간격)

Target
  - DAT : 생육 일 (1~28일차)
  - predicted_weight_g : 일별 예측한 잎 중량

Train / Test set
  - Train set: 총 28개 상추 케이스 (CASE_01 ~ CASE_28.csv)
  - Test set: 총 5개 상추 케이스 (CASE_01 ~ CASE_05.csv)

## Model
- 예측 모델: `XGBoostRegressor` 모델에 `gridsearch`로 하이퍼파라미터 튜닝
- 생성 모델: Train set 중에서 팀 내 "최적환경" 기준을 만족하는 케이스 선별 &rarr; `sdv PAR` 모델로 Input 증식 &rarr; 기존 예측모델에 Input 대입하여 Target인 'predicted_weight_g' 생성

## Feature Engineering
누적값 계산, DAT 곱, 각 변수 간 곱으로 파생변수 생성
## Feature Engineering
습도_온도
습도_온도_CO2
비료 : EC관측치 X 일간누적분무량
적산온도
습도_누적
co2_누적
ec_누적
광량_누적
비료_누적
co2_ec
총누적백색광량
총누적적색광량
총누적청색광량
총누적총광량
ec_시간당분무량
ec_일간누적분무량
ec_분무량_누적

## Team Members
- [노지예](https://github.com/kkumtori), [전민주](https://github.com/forminju), [조성우](https://github.com/jswooo), [임홍주](https://github.com/hihongju)

## Reference
- PAR
https://sdv.dev/SDV/api_reference/timeseries/api/sdv.timeseries.deepecho.PAR.html


#### 생성 모델 결과로부터 조성된 생육 환경 해석과 적합성 검토 등의 인사이트는 [ [왕왕상츄]_PPT자료](https://github.com/forminju/DACON_lettuce_prediction/blob/main/%5B%EC%99%95%EC%99%95%EC%83%81%EC%B8%84%5D_PPT%EC%9E%90%EB%A3%8C.pdf)에서 확인할 수 있습니다.
