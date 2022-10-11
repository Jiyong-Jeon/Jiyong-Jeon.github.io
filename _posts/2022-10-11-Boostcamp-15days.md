---
title: Boostcamp 15days
date: 2022-10-11 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [3weeks, 15day]
math: true

---
# 15일차 학습 정리

<h3 data-toc-skip> Semantic segmentation </h3>

- 이미지내에 픽셀들을 카테고리 구분하는 것
  - Computational photography, Medical images, Autonomous driving
- **Architectures**
  - FCN(Fully convolutional networks)
    - FC layer를 Convolutional layer(1x1 conv)로
    - Upsampling
      - resolution을 맞춤
      - Transpose conv, Upsampling conv
    - 중간단계의 activation map을 합쳐서 사용
  - Hypercolumns
    - FCN과 매우 유사 but, end to end 가 아님
    - 바운딩 박스를 적용
  - U-Net
    - 영상의 일부분을 자세히 봐야하는 경우 U-Net의 기원이 많음
    - 낮은층과 높은층의 피쳐를 적절히 결합하는 방법 연구
    - Contracting path
      - CNN
    - Expanding path
      - Upsampling
      - activation map들을 concat
    - 입력에서 중간 계산에 홀수가 나오면 안되는 것에 유의
  - DeepLap
    - CRFs(Conditional Random Fields)
      - 픽셀과 픽셀간의 관계를 이어준 것
    - Dilated convolution (Atrous convolution)
    - Depthwise separable convolution
      - Depthwise convolution
        - 채널을 따로 conv
      - Pointwise convolution
        - 1x1 conv를 활용하여 채널을 conv
      - 표현력을 유지하며 계산량을 획기적으로 줄임


---

# 기본 과제
- **기본 1 (Resnet Implementation Image Classification)**
  - Quickdraw datasets을 활용한 ResNet 구현
  - 구현한 ResNet과 Pretrained 모델 비교
  - 아직 제대로 해결하지못함
  
---

# git 특강

- 이고잉(egoing)님의 특강 (생활코딩)
- 깃을 활용한 버전관리 방법 강의
- 복습 해보기
  1. 프로젝트를 만든다.
  2. 저장소를 만든다.
  3. 파일을 만들고 2개의 커밋을 만든다.
  4. 과거 커밋을 갔다가 돌아온다. (시간여행)
  5. 브랜치 생성
  6. 서로 다른 브랜치에서 작업
     - exp 브랜치, master브랜치
  7. 브랜치 병합

---

# 피어세션
- 팀 대회
  - CNN과 kobert를 활용한 multimodal 모델 구현
    - but, 성능이 좋지못함
    - 코드를 공유하고 이유를 찾아보기로 함
- 주말간 뭐했는지 공유 등 잡담
- [회의록](https://night-eustoma-5f3.notion.site/10-11-98f2e59c369049bb988ad89087269e22)

---

### 참고자료
- 부스트캠프 AI Tech 교육 자료