---
title: Boostcamp 24days
date: 2022-10-24 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [6weeks, 24day]
math: true

---

# 타운 홀 미팅
- P-stage 프로젝트 안내
  - Special Mission
  - 실전 프로젝트
    - 그라운드룰
    - 데이터셋 저작권 주의!
      - 마스크 착용 여부 / 성별 / 나이 데이터
    - 마스크 착용 여부 판별
  - 플랫폼 사용 설명

---

# 24일차 학습 정리

<h3 data-toc-skip> Competition with AI Stages </h3>

- **P-stage**
  - U-stage에서 배운 것들을 실습해보는 과정
  - Competition이라는 과정을 통해 점진적인 모델 성능 향상을 경험
- **Competition**
  - 여러 데이터 및 task를 경험할 수 있음
  - 주어진 데이터를 이용해 원하는 결과를 만들기 위한 가장 좋은 방법들을 공유
  - Overview
    - Competition의 목적, 의미, 배경, 문제점 등등 *방향성*이 중요
    - *Problem Definition*을 하는것이 중요
  - Data Description
    - 데이터 스펙 요약본
      - File 형태, Matadata Field
  - Notebook
    - 데이터 분석, 학습, 추론 과정을 서버에서 연습 가능
  - Submission & Learderboard
    - 테스트 예측 결과물 제출 & 순위 확인
  - Discussion
    - 등수가 중요한 것이 아님
    - 문제를 해결하고 싶은 마음으로 공유하는 것이 실력 향상에 큰 도움을 줄 것

<h3 data-toc-skip> Image Classification & EDA </h3>

- Data Analysis 부분
- **EDA(Exploratory Data Analysis)**
  - 데이터를 이해하기 위한 노력
  - 목적
    - 궁금한 것(주제와 연관성, 분포, 타입의 특성 등)을 Checking 

- **Image Classification**
  - Image
    - 시각적 인식을 표현한 인공물(Artifact)
  - Model
    - Input + Model = Output
    - Input 타입과 Output 타입을 잘 구분하는 것이 중요
    - Image Classification Model
      - Image + Classification Model = Class

<h3 data-toc-skip> Dataset </h3>

- Data processing
- 데이터를 내가 원하는 데이터 셋으로 변환
- Pre-processing
  - 실제로 가장 많이 소요되는
  - 실제 데이터의 품질이 항상 좋지 않음
  - Bounding box
    - 필요한 부분만 학습
  - Resize
    - 계산의 효율을 위해 적당한 크기로
  - 도메인, 데이터 형식에 따라 다양한 방법이 존재
    - 적절한 pre-process 방식을 찾는 것도 중요
- Generalization
  - Bias & Variance
    - Underfitting, Overfitting
  - Train / Validation
    - train set / validation set / test set
    - 일반화를 판단하기 위해 분리
  - Data Augmentation
    - 데이터를 일반화하는 과정
    - 주어진 데이터의 경우, 상태 등을 다양하게
    - 라이브러리
      - trochvision.transforms, Albumentations
- 주제(Problem)을 잘 정의하고 그에 따라서 *실험으로 증명*해야 함

<h3 data-toc-skip> Data Generation </h3>

- Data Feeding
  - Feed(먹이를 주다) == 대상의 상태를 고려해서 적정한 양을 준다.
  - 모델의 구조와 상태를 고려해서 그에 맞는 데이터를 줘야함
  - Data generater -> Model (처리 속도 테스트 필요)
- torch.utils.data(라이브러리)
  - Dataset 기본 구조
    - 생성자, getitem, len (상속)
  - DataLoader
    - Dataset을 효율적으로 사용할 수 있도록 관련 기능 추가
    - 기능이 많음
      - batch, shuffle, sampler, collate_fn 등등
  - Dataset과 DataLoader는 분리되는 것이 좋다
    - 엄연히 하는일이 다름

<h3 data-toc-skip> Model </h3>

- Modeling 파트
- 시스템을 원하는 형식으로 표현해주는 것
- Design Model with Pytorch
  - Pytorch
    - Low-level, *Pythonic*, Flexibility
  - nn.Module
    - Pytorch 모델, 모든 레이어는 nn.Module을 상속받음
    - Modules
      - 모듈 안의 모듈들을 모두 출력함
    - forward
      - 모듈(모델)이 호출되었을 때 실행되는 함수
    - 모든 모듈은 child 모듈을 가질 수 있음
    - 모델을 정의하는 순간 모델에 연결된 모든 모듈을 확인할 수 있음
    - 모든 모듈은 forward함수를 가짐
    - Parameters
      - modules가 가지고 있는 계산에 쓰일 파라미터
      - data, grad, requires_grad 변수 등을 가짐

---

# 피어세션
- 오프라인 참여
  - 운영진님들과의 대화
- 수업 관련
  - 일주일 계획 세우기
  - 먼저 강의를 듣고 P-stage에 참여
- P-stage
  - 공략 및 계획 수립
- [회의록](https://night-eustoma-5f3.notion.site/10-24-7fb4c7187a864dac9bfbd485fdadec06)

---

### 참고자료
- 부스트캠프 AI Tech 교육 자료