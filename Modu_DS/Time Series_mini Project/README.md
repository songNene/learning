# Time Series Classification Mini Project

## 프로젝트 요약

| 항목               | 내용 |
|--------------------|------|
| **프로젝트 목표** | - 비정상 시계열 데이터를 정상화<br>- tsfresh로 feature 추출<br>- 다양한 분류 모델로 고장 여부 분류 |
| **사용 데이터**    | AirPassengers.csv (월별 항공 승객 수) |
| **정상화 과정**    | - 로그 변환<br>- 차분(differencing)<br>- 계절 차분<br>- ADF 단위근 검정 |
| **특징 추출 방식** | tsfresh의 EfficientParameters 이용 |
| **주요 특징**      | `F_X_abs_energy` 가 가장 높은 중요도를 보임 |
| **사용 모델**      | Logistic Regression, Random Forest, XGBoost, Gradient Boosting |

---

## 모델 성능 비교

| 모델                    | 정확도 (Accuracy) | Ture (정확도/재현율) | False (정확도/재현율) | 특징 |
|-------------------------|-------------------|------------------------|-------------------------|------|
| **Logistic Regression** | 57.14%            | 1.0 / 0.44             | 0.36 / 1.0              | 비대칭 예측 발생 |
| **Gradient Boosting**   | 95.24%            | 1.0 / 0.94             | 0.83 / 1.0              | 균형 잡힌 성능 |
| **XGBoost**             | 100%              | 1.0 / 1.0              | 1.0 / 1.0               | 과적합 또는 데이터 누수 의심 |

---

## 분류 리포트 주요 개념

| 지표            | 설명 |
|------------------|------|
| **Precision**     | 예측한 것 중 맞은 비율 |
| **Recall**        | 실제 정답 중 맞춘 비율 |
| **F1-score**      | Precision과 Recall의 조화 평균 |
| **Support**       | 클래스별 실제 샘플 수 |
| **Macro avg**     | 클래스별 단순 평균 |
| **Weighted avg**  | 클래스별 가중 평균 (support 기반) |
| **Accuracy**      | 전체 예측에서 맞춘 비율 |

---

## 사용 라이브러리

| 라이브러리       | 용도 |
|------------------|------|
| `pandas`         | 데이터 처리 |
| `numpy`          | 수치 계산 |
| `matplotlib`     | 시각화 |
| `scikit-learn`   | 모델 학습 및 평가 |
| `tsfresh`        | 시계열 특징 추출 |
| `xgboost`        | XGBoost 모델 학습 |
