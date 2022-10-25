---
title: Boostcamp 25days
date: 2022-10-25 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [6weeks, 25day]
math: true

---
# 25일차 학습 정리

<h3 data-toc-skip> Pretrained Model </h3>

- 획기적인 알고리즘 개발과 검증을 위해 높은 품질의 데이터셋은 필수
- 배경
  - 일반화를 위해 매번 수 많은 이미지를 학습시키는 것은 비효율적
  - 미리 학습된 모델은 내가 사용할 task에 맞춰 다듬어 사용
- **torchvision.models**
  - 손쉽게 모델 구조와 Pretrained weight를 다운할 수 있음
- **Transfer Learning**
  - 내 데이터, 모델과 Pretrained model의 유사성을 고려
    - Trainable, Freeze 영역 구분 (fine-tuning)
  - CNN base 모델 구조(Simple)
    - Input + CNN Backbone + Classifier(fc) = Output

<h3 data-toc-skip> Training & Inference </h3>

- **Loss**
  - 오차 역전파에 오차를 계산
  - nn.Module Family
    - 특별한 loss를 만들 수 있음
  - .backward()
    - 모델의 파라미터 gard값이 업데이트 (required_grad=false는 빼고)
  - 특별한 loss
    - Focal Loss
      - Class Imbalance 문제가 있는 경우 맞춘 확률이 낮은 Class에 높은 loss를 부여
    - Label Smoothing loss
      - class target label을 Onehot으로 표현하지 않고 Soft하게 표현([0.025, 0.9, 0.2, ...])
- **Optimizer**
  - 업데이트, 학습을 어느 방향으로 얼마나 할지 결정
  - LR scheduler
    - 학습시 Learning rate를 동적으로 조절
    - StepLR
      - 특정 Step마다 LR 감소
    - CosineAnnealingLR
      - Cosine함수 형태처럼 LR을 급격히 변경
    - ReduceLROnPlateau
      - 더 이상 성능 향상이 없을 때 LR 감소
- **Metric**
  - 객관적인 지표를 만들어 모델을 평가하기 위함
  - 모델의 평가
    - Classification
      - Accuracy, F1-score, precision, recall, AUC-ROC
    - Regression
      - MAE, MSE
    - Ranking
      - MPR, MDCG, MAP
  - 데이터 상태에 따라 올바른 Metric을 선택하는 것도 중요
    - 평가가 제대로 되었는지 확인 필수
- **Process**
  - 학습과 추론 프로세스의 과정
  - 학습과정
    1. 모델을 train모드로 바꾼다 (model.train())
       - 모드마다 optimizer나 다른 설정 등이 따로해야 성능이 높은 논문이 있음 (찾아보기)
    2. 파라미터들이 가진 gard를 초기화한다 (optimzer.zero_grad())
       - 하지않으면 loss가 더해짐 
    3. loss 계산 
       - loss를 마지막으로 chain 생성 (gard_fn chain)
    4. gard 계산, 역전파 (loss.backward())
    5. 가중치 업데이트 (optimizer.step())
  - Gradient Accumulation
    - 배치사이즈가 중요한 task에서 loss를 중첩시킨 다음에 학습시켜 배치사이즈를 크게하도록 학습
    - 이외에도 여러가지로 응용가능
  - 추론과정
    1. 추론 모드로 바꾼다 (model.eval())
    2. tensor의 grad 계산을 막는다 (with torch.no_grad())
    3. validation 셋으로 확인
        - Checkpoint는 직접 짜기 쉬움
    4. 최종 Output, Submission 형태로 변환
- **Pytorch Lightning**
  - Keras 처럼 코드를 간단하게 해준 라이브러리

<h3 data-toc-skip> Ensemble </h3>

- **Ensemble**
  - 서로 다른 여러 학습 모델을 사용하여 더 나은 성능을 이끌어 내는 기법
  - boosting, bagging 등 underfiting, overfiting의 상황에 따라 기법이 다양함
  - Model Averaging(Voting)
    - 여러 모델들의 결과를 통해 하나의 결과로 추론
  - Cross Validation
    - Stratified K-Fold Cross Validation
      - split 시 class 분포를 고려하여 Fold 진행
  - TTA (Test Time Augmentation)
    - 테스트 이미지를 Augmentation 후 추론하여 여러가지 결과를 앙상블
  - 성능과 효율의 Trade-off
- **Hyperparameter Optimization**
  - 방식론은 많음 (찾아보기)
  - Optuna 라이브러리

<h3 data-toc-skip> Experiment Toolkits & Tips </h3>

- **Training Visualization**
  - 학습 과정을 기록하고 트래킹
  - Tensorboard
    - 학습률, 이미지 등 여러가지를 추가가능
  - Weight and Bias (wandb)
- **Machine Learning Project**
  - Jupyter Notebook
    - 코드를 Cell단위로 빠르게 실행해 볼 수 있는 것이 장점
    - EDA를 할 때 매우 유용
  - Python IDLE
    - 구현을 한번만 하여 재사용을 언제든 할 수 있는 것이 장점
    - 디버깅을 할 수 있음 
    - 실험 핸들링을 자유롭게 (config)
- **Tips**
  - 분석 코드보다는 설명글을 유심히 보기
    - 필자가 생각하는 흐름을 읽기
  - 코드를 볼 때는 디테일한 부분까지
    - 언제든지 직접 활용할 수 있을 정도로
  - Paper with Codes
    - 최신 논문과 코드 잘 파악
  - 공유하는 것을 주저하지 말기
    - 공유 == 새로운 배움의 기회

---

# 피어세션
- 수업 관련
  - 강의를 미리 전부 듣고 강의에 대한 질문 공유
- P-stage
  - 데이터 분석
  - 개인 서버 환경 설정
- [회의록](https://night-eustoma-5f3.notion.site/10-25-d7d98f2b0e464fe8bdc75650fda832a6)

---

### 참고자료
- 부스트캠프 AI Tech 교육 자료