# 멋진 단어사전 만들기

이 프로젝트는 자연어처리(NLP)의 핵심 전처리 과정인 **토큰화(Tokenization)** 를 직접 구현하고,  
텍스트를 정수 시퀀스로 변환하는 과정을 실습하기 위한 목적의 학습 노트북입니다.

---
## 📂 디렉토리 구조
0613_딥러닝 단어사전 만들기/    
├── korean-english-park.train.tar.gz    
├── korean-english-park.train.ko    
├── korean-english-park.train.en    
└── 멋진 단어사전 만들기.ipynb    

## 주요 학습 내용

### 1. 학습 환경 구성 및 데이터 준비
- 한국어-영어 병렬 말뭉치 중 `korean-english-park.train.ko` 파일을 GitHub에서 다운로드
- Jupyter 환경(Windows)에서 압축 해제 및 경로 설정 자동화
- 전체 문장 수, 문장 길이 분포 등 데이터 기초 분석 수행

### 2. 공백 기반 토큰화
- 문장을 공백 기준으로 분할 (`str.split()`)
- `Tokenizer`로 단어 사전 구축 및 정수 시퀀스 변환
- `pad_sequences`로 문장 길이 정규화 (padding)

### 3. 텐서 복원 (Decoding)
- `tokenizer.sequences_to_texts()` 함수로 텐서 → 문장 복원
- `tokenizer.index_word`를 활용한 수동 복원 방식도 구현

---

## 사용한 기술 스택 및 라이브러리

- Python 3.x
- TensorFlow (Tokenizer, pad_sequences)
- KoNLPy (형태소 분석기: MeCab 시도)
- matplotlib (데이터 시각화)
- os, urllib, tarfile 등 기본 패키지

---

## 데이터 출처

- [korean-parallel-corpora by jungyeul](https://github.com/jungyeul/korean-parallel-corpora)
  - `korean-english-park.train.ko` 파일 사용 (총 94,123 문장)

---

## 학습 포인트

- 자연어처리 모델 학습 전 단계인 텍스트 전처리 과정을 구현
- 토큰화 → 정수 인코딩 → 패딩 → 디코딩까지의 End-to-End 처리 흐름 이해
- 공백 기반 토큰화의 한계와 형태소 기반 방식(MeCab)의 필요성 체감
