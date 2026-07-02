# README: 딥러닝 실습 정리

본 문서는 다음 세 가지 딥러닝 실습 노트북 내용을 정리한 것이다:

* Boston Housing 주택 가격 예측
* Reuters 뉴스 분류 모델
* CIFAR-10 이미지 분류 모델

각 프로젝트는 데이터 전처리부터 모델 학습, 평가, 시각화까지 포함되어 있으며, 실습 목적에 따라 회귀 또는 다중 클래스 분류 문제로 구성되어 있다.

## 1. Boston Housing 주택 가격 예측

| 항목    | 내용                                             |
| ----- | ---------------------------------------------- |
| 데이터셋  | keras.datasets.boston\_housing                 |
| 문제 유형 | 회귀 (주택 가격 예측)                                  |
| 특성 수  | 13개 특성 (예: 주택 크기, 위치 등)                        |
| 전처리   | 평균 및 표준편차 기반 표준화 (train, test 모두 동일 방식 적용)     |
| 모델 구성 | Dense(64) - ReLU - Dense(64) - ReLU - Dense(1) |
| 손실 함수 | MSE (Mean Squared Error)                       |
| 평가 지표 | MAE (Mean Absolute Error)                      |
| 학습 전략 | EarlyStopping, ModelCheckpoint 적용              |

## 2. Reuters 뉴스 분류 모델

| 항목     | 내용                                                                                                                                |
| ------ | --------------------------------------------------------------------------------------------------------------------------------- |
| 데이터셋   | keras.datasets.reuters                                                                                                            |
| 문제 유형  | 다중 클래스 분류 (46개 뉴스 카테고리)                                                                                                           |
| 입력 처리  | 원-핫 인코딩 (10,000 차원 벡터)                                                                                                            |
| 레이블 처리 | to\_categorical()을 통한 원-핫 인코딩                                                                                                     |
| 모델 구성  | Dense(128) - ReLU - BatchNormalization - Dropout(0.2) - Dense(64) - ReLU - BatchNormalization - Dropout(0.2) - Dense(46, softmax) |
| 손실 함수  | categorical\_crossentropy                                                                                                         |
| 평가 지표  | accuracy                                                                                                                          |
| 학습 전략  | EarlyStopping, ModelCheckpoint 적용                                                                                                 |

## 3. CIFAR-10 이미지 분류 모델

| 항목     | 내용                                                                                          |
| ------ | ------------------------------------------------------------------------------------------- |
| 데이터셋   | keras.datasets.cifar10                                                                      |
| 문제 유형  | 다중 클래스 이미지 분류 (10개 클래스)                                                                     |
| 입력 처리  | 32x32x3 이미지를 3072차원 벡터로 reshape                                                             |
| 클래스 라벨 | \['airplane', 'automobile', 'bird', 'cat', 'deer', 'dog', 'frog', 'horse', 'ship', 'truck'] |
| 모델 구성  | Dense(512) - ReLU - Dense(256) - ReLU - Dense(10, softmax)                                  |
| 손실 함수  | sparse\_categorical\_crossentropy (레이블은 정수형)                                                |
| 평가 지표  | accuracy                                                                                    |
| 학습 전략  | EarlyStopping, ModelCheckpoint 적용                                                           |

## 공통 시각화 항목

* 학습 과정의 `loss`, `val_loss`, `accuracy`, `val_accuracy`를 시각화
* matplotlib를 사용해 두 개의 subplot으로 시각화 (Loss/Accuracy)

## 기타 정리 사항

* 학습은 각 문제에 적절한 batch\_size를 실험적으로 조정하여 진행함 (예: 64, 128 등)
* 입력 형식에 따라 손실 함수가 다르게 지정되었으며, 모델에 맞춰 조정함
* 학습 도중 과적합 방지를 위해 조기 종료와 최적 가중치 저장 로직이 일관되게 적용됨

---

모든 노트북은 keras 기반의 Sequential 모델을 사용했으며, 데이터 분리는 `train_test_split()`을 활용했다. 입력 전처리 및 출력 인코딩 방식은 문제 유형에 따라 다르게 적용되었다.

