# AutoInt+ 기반 영화 추천 시스템

## 프로젝트 개요

본 프로젝트는 모두의 연구소에서 진행한 학습 프로젝트로 MovieLens 1M 데이터셋을 기반으로 사용자의 영화 평가 이력을 바탕으로 개인화된 추천 시스템을 구축하는 것을 목표로 합니다.  
대표적인 딥러닝 기반 추천 모델인 **AutoInt+**를 직접 구현하고, 다양한 하이퍼파라미터 튜닝을 통해 성능을 향상시키며, 최종 결과는 **Streamlit 앱**을 통해 시각화하였습니다.

---

## 사용한 모델: AutoInt+

AutoInt+ 모델은 다음과 같은 구조로 구성됩니다.

- **Embedding Layer**: 범주형 데이터를 밀집 벡터로 임베딩  
- **Multi-Head Self-Attention**: feature 간 복잡한 상호작용을 학습  
- **Residual Connection**: 학습 안정성과 성능 향상  
- **MLP Layer**: 고차원의 feature를 통합  
- **Output Layer**: 이진 분류 (좋아요/싫어요)

TensorFlow의 `tf.keras.Model` 기반으로 모델을 정의하였습니다.

---

## 최종 모델 파라미터

| 파라미터       | 값          |
|----------------|-------------|
| Epochs         | 20          |
| Learning Rate  | 5e-4        |
| Dropout        | 0.2         |
| Batch Size     | 1024        |
| Embedding Dim  | 32          |
| Optimizer      | Adam        |

---

## 폴더 구조

```text
autoint    
├── autointmlp.py    
├── show_st2.py    
├── data    
│ ├── field_dims.npy    
│ ├── autoIntMLP_label_encoders.pkl    
│ ├── movielens_rcmm_v2.csv    
│ └── ml-1m    
│   ├── movies_prepro.csv    
│   ├── ratings_prepro.csv    
│   └── users_prepro.csv    
├── model    
  └── autoIntMLP_model_weights.weights.h5   
```

---

## 모델 성능 실험 기록

| 실험 번호 | Epoch | Learning Rate | Dropout | Batch Size | Embedding Dim | NDCG   | Hitrate |
|-----------|--------|----------------|---------|-------------|----------------|--------|---------|
| 기본값    | 5      | 1e-4           | 0.4     | 2048        | 16             | 0.6617 | 0.6298  |
| 실험 1    | 20     | 1e-4           | 0.4     | 2048        | 16             | 0.6618 | 0.6303  |
| 실험 2    | 20     | 1e-4           | 0.2     | 1024        | 32             | 0.6663 | 0.6325  |
| 실험 3    | 20     | 5e-4           | 0.2     | 1024        | 32             | **0.6667** | **0.6352**  |

- 실험 3이 가장 높은 성능을 기록하였으며, 해당 파라미터를 최종 모델로 채택하였습니다.

---

## 실행 방법

```bash
# 라이브러리 설치
pip install -r requirements.txt

# Streamlit 앱 실행
streamlit run show_st2.py
