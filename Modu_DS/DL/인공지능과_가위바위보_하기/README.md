# 딥러닝 첫걸음 – MNIST 손글씨 분류 실습

이 프로젝트는 모두의연구소에서 제공한 딥러닝 학습 노드를 따라 진행한 실습 내용입니다.  
MNIST 손글씨 숫자 데이터를 활용해 CNN(합성곱 신경망) 기반 이미지 분류 모델을 구현하고,  
TensorFlow와 Keras의 Sequential API를 사용해 학습 및 평가를 수행하였습니다.

---

## 프로젝트 개요

- **목표**: 손글씨 숫자 이미지(0~9)를 분류하는 딥러닝 모델 학습
- **데이터셋**: [MNIST](http://yann.lecun.com/exdb/mnist/) – 28x28 흑백 손글씨 이미지
- **프레임워크**: TensorFlow 2.x, Keras
- **모델 구조**: CNN + Fully Connected Layer
- **학습 기반**: 모두의연구소 딥러닝 입문 노드

---

## 데이터 정보

- 총 70,000장 이미지 (28x28 픽셀, grayscale)
  - 학습용: 60,000장
  - 테스트용: 10,000장
- 레이블: 숫자 클래스 (0~9)

---

## 모델 구조 (Sequential)

```python
model = models.Sequential([
    layers.Conv2D(32, (3, 3), activation='relu', input_shape=(28, 28, 1)),
    layers.MaxPooling2D(2, 2),
    layers.Conv2D(64, (3, 3), activation='relu'),
    layers.MaxPooling2D(2, 2),
    layers.Flatten(),
    layers.Dense(64, activation='relu'),
    layers.Dense(10, activation='softmax')
])
