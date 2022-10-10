---
title: Boostcamp 15(1)days
date: 2022-10-10 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [4weeks, 15(1)day]
math: true

---
# 15(1)일차 학습 정리
공휴일 및 공결 대비 학습

<h3 data-toc-skip> 컴퓨터 비전 </h3>

- Input : visual data(Image or Video)
- **Tasks**
  - Color, Motion, #D, Semantic-level, Social(emotion), Visuomotor perception & etc.
  - 인간의 시각적 불안정한 부분까지
- CNN은 많은 CV Task들의 Backbone으로 사용됌
- **CNN architectures history**
  - 이전 수업 복습
    - AlexNet, VGGNet
    - 레이블을 깊게 쌓으려는 노력을 하였으나 깊게 쌓을 수록 문제들이 발생
      - Gradient vanishing/exploding, Computationally complex, Degradation problem
    - GoogLeNet, ResNet
    - Beyond ResNets (DenseNet, SENet)
    - EfficientNet
      - deep, wide, high resolution 요소 3가지를 적절히 조합
- **Deformable convolution**
  - irregular shape 을 위한 conv

<h3 data-toc-skip> Data Augmentation </h3>

- 데이터셋은 거의 항상 편향되어있음
  - 데이터 셋 샘플은 실제 데이터를 표현할 수 없음
  - 데이터 셋이 실제 데이터를 표현할 수 있도록 변형하는 것이 Augmentation
- Augmentation 방법
  - 밝기, 기하학 변환(회전, 반전, Affine), Crop, CutMix 등등
  - RandAug
    - 여러가지 가능한 기법을 조합하여 가장 좋은 augmentation 조합(policy)을 찾는것
- Transfer learning
  - 이미 학습 시켜놓은 모델로 작은 데이터만으로 높은 성능을 끌어내는 방법
- Knowledge distillation
  - 이미 학습된 큰 모델에서 작은모델로 지식을 전달
    - 모델 압축
    - 큰 모델이 pseudo-labeling을 하여 큰 데이터 셋을 만들고 작은 모델을 학습
  - 방식
    - 큰 모델의 아웃풋을 따라하게 하는 방식
      - 레이블을 사용하지 않음 (unsupervised)
    - 큰 모델을 따라하는 loss와 실제 레이블과의 차이를 나타내는 loss
      - Softmax with Temperature 사용
      - Student Loss
        - CrossEntropy loss
        - Hard label 사용
        - 정답을 맞추도록 학습
      - Distillation Loss
        - KL div loss
        - Soft label 사용
        - Teacher model을 따라하도록 학습
- Semi-supervised learning
  - labeled된 작은 데이터와 unlabeled된 큰 데이터를 사용
  - 방식
    - labeled된 작은 데이터로 모델을 생성
    - unlabeled 데이터에 pseudo-labeled 생성
    - 이를 활용하여 다른 모델을 생성
- self-training
  - Augmentation + Teacher-Student networks + semi-supervised learning
  - 방식
    - 그림
    - 해당 과정을 반복
    - 이때, Student model은 점점 커지는 방향으로 설계


---

# 일반 과제
- AAE (Adversarial Autoencoder)
  - AAE 논문의 설명에 맞게 모델 구축 실습
  - 완벽히 이해하지 못해 AAE논문과 그에 관련된 논문을 읽어봐야할 듯

---

# 피어세션
- 공휴일

---

### 참고자료
- 부스트캠프 AI Tech 교육 자료