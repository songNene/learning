# 인공지능과 가위바위보 하기 

본 프로젝트는 딥러닝 모델을 활용하여 이미지 기반의 가위바위보 분류 모델을 만들고 학습하는 과정을 담고 있습니다. TensorFlow 2.6.0 환경에서 진행되었으며, 직접 수집한 이미지 데이터를 사용하여 모델을 훈련하고 테스트합니다.

## 프로젝트 개요

- **목표**: 28x28 이미지로부터 '가위', '바위', '보'를 분류할 수 있는 인공지능 모델 만들기
- **데이터**: 직접 수집한 JPG 이미지 (scissor, rock, paper 폴더로 구성)
- **모델 구조**: CNN 기반의 딥러닝 모델
- **라이브러리**: TensorFlow, NumPy, PIL, Matplotlib 등

## 사용 라이브러리

```python
import tensorflow as tf
from tensorflow import keras
import numpy as np
import matplotlib.pyplot as plt
import os
from PIL import Image
import glob
