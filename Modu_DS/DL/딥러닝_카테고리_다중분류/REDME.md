# 뉴스 카테고리 다중 분류 (Reuters Dataset 기반)

이 프로젝트는 Reuters 뉴스 데이터를 활용하여 텍스트 다중 분류 문제를 해결하는 실습입니다.     
텍스트 벡터화를 거친 후 다양한 머신러닝 모델을 적용해 분류 성능을 비교합니다.

---

## 사용한 데이터셋
- **Reuters Newswire Topics Dataset (로이터 뉴스 데이터)**
- 총 **46개 클래스**
- 뉴스 본문을 숫자 시퀀스로 변환한 형태 제공
- `tensorflow.keras.datasets.reuters` 에서 제공

---

## 전처리 및 모델링 개요

- 단어 수 제한: 상위 10,000개 빈도 단어만 사용 (`num_words=10000`)
- 학습: 80%, 테스트: 20%
- 각 뉴스 문장은 숫자 인덱스 리스트로 구성되어 있으며, 텍스트로 복원 가능
- 레이블은 0~45 범위의 정수 (총 46개 클래스)

---

## 사용한 분류 모델

1. **로지스틱 회귀 (Logistic Regression)**
   - 패널티: L2
   - 다중 클래스용 `multi_class='multinomial'`
   - `max_iter=1000` 지정으로 수렴 처리

2. **서포트 벡터 머신 (SVM)**
   - `LinearSVC` 사용
   - `C=1.0`, One-vs-Rest 전략

3. **랜덤 포레스트 (RandomForestClassifier)**
   - `n_estimators=100`
   - `max_depth=None`

4. **Gradient Boosting Classifier**
   - `learning_rate=0.1`
   - `n_estimators=100`

5. **Complement Naive Bayes**
   - `alpha=1.0`
   - 희소 행렬 기반 분류에 적합

6. **VotingClassifier (Soft Voting)**
   - 위 모델 중 일부 조합하여 soft voting 수행
   - 구성:
     - Logistic Regression
     - Complement Naive Bayes
     - GradientBoostingClassifier
   - 약 **30분 이상 로컬 환경에서 학습 소요**

---

## 성능 평가 지표

- **Accuracy**
- **F1-score (macro average)**
- **Confusion Matrix** 시각화
- 모델별 성능 비교

---

## 기타

- 데이터 전처리 및 TfidfVectorizer 사용
- GridSearchCV는 사용하지 않았음
- 전체 워크플로우는 Jupyter Notebook 기반

