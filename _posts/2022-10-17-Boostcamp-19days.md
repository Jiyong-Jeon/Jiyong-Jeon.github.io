---
title: Boostcamp 19days
date: 2022-10-17 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [5weeks, 19day]
math: true

---
# 19일차 학습 정리

<h3 data-toc-skip> CNN Visualization </h3>

- **CNN Visualization**
  - CNN에 내부를 시각화하여 무엇이 문제인지, 성능 개선 방향이 무엇인지 확인해보기 위함
  - Filter visualization(weight), Activation visualization(필터링 결과)
- Visualization 방법론은 모델의 이해에 중점을 둔것과 결과의 이해에 중점을 둔 것들로 나뉨
- **Feature 분석**
  - Nearest neighbors (Top 6)
  - 차원 축소 방법 (Dimensionality reduction)
    - t-SNE (t-distributed stochastic neighbor embedding)
- **Layer Activation 분석**
  - Hidden node들이 보고있는 것을 시각화
  - Maximally activating patch
    1. 분석하는 레이어를 정하기
    2. 예제 데이터를 넣고 activation map 저장
    3. maximum activation values 를 토대로 image crop
  - Class visualization (Image synthesis)
    1. 분석하는 이미지 (dummy iamge, blank or random)를 넣는다.
    2. backpropagation을 통해 타겟 스코어를 높이는 방향으로 업데이트
    3. 업데이트 된 이미지를 통해 1, 2 반복
- **Model decision explanation**
  - Saliency test
    - Occlusion map
      - Occlusion patch를 이용하여 이미지를 가리고 스코어를 측정
    - via backpropagation
      1. 입력 영상(현재 데이터)을 넣어준다
      2. 역전파를 입력 도메인까지 진행하고 기울기를 절대값을 취한다.
      3. gradient magnitude map 시각화
  - Rectified unit(backward pass)
      - backward 과정에서 음수를 마스크 (backward에 relu)
      - 혹은 forward. backward의 음수들 둘다 마스킹
  - CAM (Class Activation Mapping )
    - FC layer 대신 CAP(CAM 구조)를 학습
    - Grad-CAM 
      - 구조를 바꾸지않고 CAM을 추출하는 방법
      - backbone이 CNN이면 사용가능
- 분석이 가능하면 이후에 응용해서 더 창의적인 것들을 할 수 있다.

<h3 data-toc-skip> Autograd </h3>

- Autograd
  - forward & backward pass를 도와줌
  - backward를 두 번할 시 gradients를 accumulate
- Saliecy test 실습
  - hook을 사용하여 중간 gradients 저장

<h3 data-toc-skip> Segmentation </h3>

- **Instance segmentation**
  - Semantic segmentation + distinguishing instances
  - Mask R-CNN
    - R-CNN과 매우 유사 => Faster R-CNN + Mask branch
    - RoI Pooling (정수) 대신 RoIAlign(실수) 사용 가능
  - YOLACT
    - 싱글스테이지 구조
    - 실시간
    - YolactEdge
- **Panoptic segmentation**
  - Instance segmentation + distinguishing instances(개별)
  - UPSNet
    - Semantic & Instance head -> Panoptic head => Panoptic logits
  - VPSNet
- **landmark localization**
  - Facial landmark, Human pose 등
  - Heatmap classification 이 사용됨
    - Coordinate regresesion : 매우 부정확
  - Landmark location을 Gaussian heatmap으로 바꾸는 방법
    - $ G_\sigma (x,y) = \exp ( - \frac {(x-x_c)^2 + (y-y_c)^2}{2 \sigma ^2}) $
    - 역방향 계산도 찾아보기
  - Hourglass network
    - hourglass 모듈를 쌓아서 반복한 구조
      - hourglass = U-net과 유사
  - DensePose
    - UV map
      - 3D를 2차원으로 펼쳐놓은 것
    - 결과물로 UV map을 출력
    - DensePose R-CNN
      - Faster R-CNN + 3D surface regression branch
  - RetinaFace
    - FPN + Multitask branches
- Backbone 네트워크 위에 Target-task branch 만 바꿔도 많은것을 수행할 수 있다.
  - 요즘 CV트랜드
- **Detecting object as keypoint**
  - CornerNet
    - 좌상, 우하 점을 사용하여 바운딩 박스 추출
    - 성능보단 속도 위주
  - CenterNet
    - 1. ConrnerNet + Center
    - 2. Centeor + width, Height

<h3 data-toc-skip> Conditional generative model </h3>

- 조건이 주어지고 정답을 그리는 확률을 구하는 문제로 생각 가능
- 응용 사례
  - 해상도 오디오 해상도 변환
  - 번역
  - 주제를 주고 글쓰기
  - Image to Image translation
    - Style transfer, Super resolution, Coloization 등
- Conditional GAN
  - GAN과 비슷하지만 Condition이 입력에 추가로 주어짐
  - ![Conditional GAN](/img/post/boostcamp_19days_img_1.png)
- L1 or L2 loss vs GAN Loss
  - 평균 로스를 사용하게되면 이미지를 생성하는 과정에서 중간인 값으로 로스를 낮추려는 경향이 있음 (회색)
  - GAN loss는 discriminator을 활용, 더 명확하게 학습 (검정, 흰)
- Image translation GANs
  - Pix2Pix
    - Total loss (GAN loss + L1 loss)
      - $ G^* = \arg \underset{G}{\min} \underset{D}{\max} L_{cGAN}(G,D) + \lambda L_{L1}(G)$
  - CycleGAN
    - non-pairwise datasets 사용
    - 두 도메인 사이의 변환을 해줌
    - CycleGAN loss = GAN loss + Cycle-consistency loss
      - $L_{GAN}(X\rarr Y) + L_{GAN}(Y\rarr X) + L_{cycle}(G, F)$
      - Cycle-consistency loss
        - 원본 이미지와 변환된 결과에서 다시 원본 이미지로 변환한 결과가 동일 해야한다
        - self-supervised 방법
        - 컨텐츠가 유지되게 해줌
- Perceptual loss
  - high quality output을 만들기 위함
  - GAN loss
    - 코드와 학습이 어렵다
    - Pre-trained networks는 필요 없음 (다양한 데이터에 적용 가능)
  - Perceptual loss
    - 코드와 학습이 간단
    - Pre-trained networks가 필요
  - ![구조](/img/post/boostcamp_19days_img_2.png)
  - Image Transform Net
    - input이 주어지면 transformed image 추출
  - Loss Network
    - imageNet으로 학습된 pre-trained VGG model
    - 학습하는동안 고정되어있음
  - Feature reconstruction loss
    - 변환된 이미지가 content를 유지하고 있는가
    - 변환된 이미지와 원본 이미지를 VGG network에 넣어 나온 결과 둘을 비교
    - L2 loss 사용
  - Style reconstruction loss
    - 변환할 스타일의 이미지와 변환된 이미지를 VGG에 넣어 Feature map을 비교
    - Gram matrices
      - 피처맵의 특징 통계을 모아둔 것 (공간적 특성 제외)
      - 피처의 스타일을 파악
      - 추가로 학습해보기
- Conditional GAN 응용 사례
  - Deepfake
    - face, voice 등
  - Face de-identification
    - 프라이버시
  - Face anonymization with passcode
  - Video translation
    - Pos transfer, Video to video translation, video to game 등
---

# 피어세션
- 수업 관련
  - 일주일 계획 세우기
- 알고리즘 공부
  - 구름IDE 먼데이챌린지 참가
  - 문제 해결 방법 공유
- 카카오 사태에 관한 토론
- [회의록](https://night-eustoma-5f3.notion.site/10-17-4aad6903e002448ab49a235b857ea51b)

---

### 참고자료
- 부스트캠프 AI Tech 교육 자료