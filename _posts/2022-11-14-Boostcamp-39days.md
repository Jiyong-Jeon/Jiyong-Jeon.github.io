---
title: Boostcamp 39days
date: 2022-11-14 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [9weeks, 39day]
math: true

---

# 39일차 학습 정리

<h3 data-toc-skip> Object Detection </h3>

- Real world task
  - 자율 주행, CCTV
- History
  - R-CNN 부터 SwinT 까지 다룰 예정
- Evaluation
  - 성능 : mAP, IOU
  - mAP
    - 각 클래스당 AP의 평균
    - mAP
      - Confusion matrix
      ![confusion matrix ex](/img/post/boostcamp_39days_img_1.png)
      - Precision / Recall
      - PR Curve
        - 모든 예측에 대해 Precision과 Recall을 계산하여 그래프로 나타냄
      - AP
        - PR Curve의 아래 범위
  - IoU (Intersection Over Union)
    - IoU 기준에 따라 TP/FP기준을 나눌 수 있음 (threshold)
  - 속도 : FPS, Flops
  - Flops
    - 모델이 얼마나 빠르게 동작하는지 측정하는 매트릭
    - 연산량 횟수
    - Channel 별계산, 커널 계산, 높이 너비 별 계산의 곱
- Library
  - MMDetection
    - pytorch 기반 오픈소스
  - Detectron2
    - 페이스북 AI 리서치에서 공개한 pytorch 기반 오픈소스
  - YOLO
    - coco 데이터셋으로 학습된 YOLO기반 디텍션모델
  - EfficientDet
    - EfficientNet을 응욯해 만든 디텍션 모델
- 특징
  - 통합된 라이브러리 부재
  - 복잡한 파이프라인
  - 높은 성능을 내기위해 무거운 모델을 활용
  - Resolution이 성능에 영향을 많이 끼쳐 사진의 크기가 큼

---

# level2
- 국방 AI 대회 마무리
  - 10위로 마무리
  - 본선 진출!

---

# 피어세션
- 강의 1강 리뷰
- level2 팀 외부대회
  - Instance segmentation 모델 리뷰
  - 대회 룰 정하기
- 프로젝트 주제, 팀명 정하기
- Notion 관리

---

# 오피스 아워
- level2 전체적인 일정
- level2 p-stage 내용 공개
      
---
### 참고자료
- 부스트캠프 AI Tech 교육 자료