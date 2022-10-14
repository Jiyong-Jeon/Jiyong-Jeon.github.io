---
title: Boostcamp 18days
date: 2022-10-14 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [4weeks, 18day]
math: true

---
# 18일차

<h3 data-toc-skip> Object Detection </h3>

- Classification + Box localization
- 응용 분야
  - 자동주행, OCR
- Two-stage detecter
  - Gradient-base detector (HOG)
  - Selective search (proposal box)
  - R-CNN
    - Region proposal을 추출
    - warpping 된 region을 CNN 계산
    - feature을 통해 탐색
  - Fast R-CNN
    - 영상 전체 feature map 추출
    - RoI feature 추출 (RoI Pooling layer)
    - 이를 활용하여 class와 box 추출
  - IoU
    - 두 영역의 교집합 / 두 영역을 합집합
  - Faster R-CNN
    - region proposal을 neural network 기반으로 (RPN (Region Proposal Network))
      - k개의 Anchor boxes 사용
    - Non-Maximum Suppression(NMS)
    - End to End 모델
- Single stage detector
  - RoI pooling을 사용하지 않음
  - 성능이 떨어지더라도 속도에 중점 (Real-Time detection)
  - YOLO (You Only Look Once)
  - SSD (Single Shot Multi Box Detector)
    - multi scale feature map에 따라 다양한 box를 고려할 수 있다.
- Focal loss
  - single detector 는 Class imbalance 문제가 심함
    - 배경에 대한 계산 등등
  - Cross Entropy의 확장
    - 오답일 경우 기울기가 커짐 (뾰족한 그래프)
- Retina Net
  - feature pyramid net (FPN) 활용
  - Class 와 box를 따로 계산
- Detection with Transformer
  - DETR
    - CNN과 positional encoding을 인코더 토근으로 입력
    - Object query를 decoder에 활용
      - 박스가 뭔지, 위치가 어딘지 등등


# 기본 과제
- **Classification_to_Segmentation (기본-3)**
  - VGG Backbone 구조를 활용한 Segmentation 실습
  - VGG Classification을 Segmentation으로 바꿔보기
  - 과제 의도에 대해서 이해가 되지않았지만 잘 해결함
  
---

# 스페셜 피어세션

- Level 2 팀 결성을 위한 자기소개
- 팀 빌딩 진행 사항 공유
- 각자 학습을 어떻게 진행하는지 의견 공유
- 주제선정시에 데이터 수집에 대한 토론

---

# 피어세션
- 수업 관련
  - 과제 3 의도에 대한 토론
  - 각자 해결 방법 설명
- 팀 빌딩
  - 팀 빌딩 과정 공유
- 팀 회고록 작성
- [회의록](https://night-eustoma-5f3.notion.site/10-14-44a26bbea678478a96e41ed2f33aa507)

---

# 오피스아워
- 기본과제 1, 2, 3 설명
- 과제에 대한 질의 응답

---

### 참고자료
- 부스트캠프 AI Tech 교육 자료