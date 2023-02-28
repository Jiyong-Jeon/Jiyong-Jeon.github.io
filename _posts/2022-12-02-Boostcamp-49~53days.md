---
title: Boostcamp 49~53days
date: 2022-12-02 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [11weeks, 49day, 50day, 51day, 52day, 53day]
math: true

---

# 49~53일차 학습 정리

---

# 피어세션
- level2 팀 외부대회
  - 국방 AI 본선 주제 공개 (전천후 작전수행을 위한 화상 이미지 노이즈 제거)
    - 오프라인 대회 준비
      - 오프라인 대회 전 관련 Task 찾아보기
      - 대회에서 사용할 만한 기법 정리하기
  - 오프라인 대회 출전
    - 최종 5위로 후원기업상 수상

- P-stage
  - 
- 프로젝트 주제, 팀명 정하기
  - 좀 더 경제적인 주제로

---

# 멘토링
- Object detection (P-stage) 대회
  - 대회 진행상황 공유
  - Small object를 잘 찾는 방법이 무엇일까?
    - nms --> soft nms
      - 이미지가 많이 겹쳐있음
    - score
    - 패치이미지와 원래이미지를 동시에 해본다?
  - Small object를 잘 찾는다고 좋을것인가?
  - 데이터 클린징 작업이 중요할 수 있다.
    - EDA를 다시 진행해봐야할듯

# 스페셜 피어세션
- 대회 이야기
  - 슈도 라벨링 --> 결과가 좋아지지 않았다
  - YOLO, cascade rcnn
  - detector - swin-l, 
  - img size 
    - 클수록 좋았음
    - multi scale 기능을 사용했을 때 더 좋았다.
  - confusion matrix
    - 0번 라벨이 가장 안잡힘
    - CE loss에 안잡히는 라벨에 가중치를 넣었다.
  - Loss -> 모델 자체에 포함되는 로스들이 많아서 변경하지 않음
  - bbox가 엄청 많은 이미지는 삭제해봤는데 별로였음
  - box보다 clasification이 안된 경향
    - 모델마다 경향이 달라서 앙상블
  - soft nms, nms는 nms가 더 높았음
    - iou score 0.05 or 0
  - 앙상블 효과
    - k-fold 앙상블 효과가 좋았음
  - swin tranforemr
    - mosaic 맞지않음
  - classification 이 더 문제였음
  - rcnn 
  - datasets을 직접 건드림
    - coco anotator, robo flow
    - 데이터를 만질수록 떨어지는 경향
---

# 마스터 클래스
- 대회 랩업 - 솔루션 발표, 피드백, 질의응답
- 상위 팀 발표
  - EDA
    - 이미지별, bbox개수 및 크기 상이 -> validation set을 구분할 때 사용
    - bbox aspect ratio 분석 -> anchor box ratio 설정에 사용
  - Augmentation 실험
    - RandomRoatate90(elicpse rotate), Resizedcrop
    - mosaic
    - CLAHE
    - mix up -> 성능 저하
  - Model
    - cascade swin
    - YOLO
  - TTA & Ensemble
    - TTA
      - multiscale, flip
    - Ensemble
      - 앙상블시 가중치를 주어
  - 이외 시도
    - 데이터 클리닝
    - 2step training
      - 작은 박스만 따로 학습
    - pseudo labeling
    - soft teacher
  - 피드백
- 1위 팀 발표
  - 누구보다 많은 실험을 하기위해 노력
    - notion을 이용하여 실험당 내용을 비교
  - augmentation
    - Multiscaling -> DETR augmentation 전략
    - HueSaturationValue
    - GaussNoise
  - model
    - 많은 모델들을 사용함
    - backbone만 pretrained를 사용하는 것이 아닌 head와 neck도 pretrained 모델을 사용
    - YOLO7, swin+cascade, swin+byhead, swin-large => ensemble
    - Convnext Net 모델이 높은 향상을 보임
  - eval
    - score thr = 0.05  -> 낮을 수록 높은 성능을 내는 경향
  - ensemble
    - 높은 성능을 보인 모델에 대해 가중치
- 대회 이후 사용된 방법에 대해 paper들을 리뷰해보는 것들이 중요
- 대회를 마무리하는 과정이 중요하다
- 이후 discussion
  - 데이터 분석 전략
    - 라벨링 오류에 대처하는 방법은 없었을 까?
  - 모델 학습 전략
    - 논문? 다 볼 순 없다. 필요한 것만 보자
  - 엔지니어링 테크닉
  - 힘들었던점
  - 동료학습

---
### 참고자료
- 부스트캠프 AI Tech 교육 자료