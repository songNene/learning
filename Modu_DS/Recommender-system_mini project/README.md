# Movielens 기반 Session-Based Recommendation System

이 프로젝트는 Movielens 1M 데이터를 기반으로, **세션 기반 추천 시스템(Session-Based Recommendation)** 을 구현한 실습입니다.  
명확한 Session ID가 존재하지 않는 상황에서 `UserId`를 session처럼 간주하여 시퀀스 데이터를 구성하고,  
**GRU 기반의 RNN 모델을 사용하여 다음에 소비할 아이템을 예측**합니다.

---

## 📁 프로젝트 구조
├── Movielens 영화 SBR - Project.ipynb # 전체 구현 및 실험이 담긴 노트북    
└── README.md    

---

## 주요 구현 내용

### 1. 데이터 로딩 및 전처리

- `ratings.dat` 불러오기 (`::` 구분자 사용)
- 평점(Rating) 3 이상만 필터링
- Time 컬럼은 `datetime` 형식으로 변환
- 세션 단위 정의: `UserId`를 SessionId처럼 사용, 시간 순 정렬
- 짧은 세션/희소한 아이템 제거: `cleanse_recursive()` 함수 사용

### 2. 데이터 분할

- 전체 데이터를 기준으로 최근 7일을 기준으로 validation/test 분할
- 세션별 시간 흐름을 보존하기 위해 `split_by_date()` 활용
- 총 2번 분할하여 `train`, `val`, `test` 구성

### 3. 모델 구성

- GRU 기반 시퀀스 모델  
  구조: **GRU → Dropout → Dense(Softmax)**
- 세션별 hidden state 초기화를 통해 session-parallel 학습 설계
- Keras + TensorFlow 기반 학습 루프 구성

### 4. 학습 및 평가

- `train_model()` 함수에서 epoch별 loss / recall@k / mrr@k 출력
- 실험 조건 변경:
  - `batch_size` 변화 (e.g. 128, 256 등)
  - `epoch` 수 조정
  - 전처리 조건 변경 (`shortest`, `least_click`)
- 평가 지표:
  - **Recall@20** : 상위 20개 예측 중 실제 클릭이 포함되었는지
  - **MRR@20** : 정답 아이템이 상위 20개 예측에서 몇 번째에 있는지의 역순위 평균

---


## 느낀 점

- 세션 기반 추천 시스템은 단순한 추천보다 **사용자 행동 흐름의 맥락을 더 정밀하게 반영**해야 한다는 점에서 흥미로웠습니다.
- 전처리의 작은 변화, 배치 크기, epoch 수 등의 조정이 성능에 영향을 크게 줄 수 있어 **실험 설계의 중요성**을 체감했습니다.
- 수치상 성능은 조금씩 개선되었지만, **확연한 드라마틱한 변화가 없어서 다소 아쉬움이 남는 실험**이었습니다.
- 그럼에도 불구하고 실험을 반복하며 결과를 관찰하는 과정이 모델의 특성과 데이터의 구조를 이해하는 데 큰 도움이 되었습니다.

---

## 주요 기술 스택

- Python 3.x
- Pandas, NumPy
- TensorFlow, Keras
- tqdm
