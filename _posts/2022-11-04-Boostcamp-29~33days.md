---
title: Boostcamp 29~33days
date: 2022-11-04 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [7weeks, 29day, 30day, 31day, 32day, 33day]
math: true

---
# 29~33일차 P-stage

<h3 data-toc-skip> EDA </h3>

- Dataset 분석
  - 노이즈 검사
    - 성별, 나이, 라벨링 오류 검사
  - PCA 공부 (참고 : [PCA 참고](https://365datascience.com/tutorials/python-tutorials/pca-k-means/))
- Dataset 시각화


<h3 data-toc-skip> Baseline code 분석 및 Custom </h3>

- StratifiedKFold 구현
  - KFold에 맞는 Custom Dataset 구현
  - Out of Fold
- early stop 구현
- imbalanced Dataset Sampler
- LADE Loss 구현
- 문제는 Age 분류!

<h3 data-toc-skip> new Baseline 제작 </h3>

- 모델 분리
  - Age Model
    - 3분류(30이하, 30~60, 60이상)가 아닌 5살 기준 10분류(15~20 , 20~25, ··· , 60~65)로 나누어 학습
    - 10분류 -> 3분류 변환
  - MultiModel
    - Mask + Gender multi head
  - BatchNormlayer 추가
  - 사용 모델
    - SwinTransformer, ResneXt 비교
- Optimizer
  - Adam, AdamW, AdamP
- Augmentation
  - RandomCrop 추가
  - CHALE 추가
- Imbalance Sampler
- Loss
  - Focal, F1, LADE

---

# 멘토링
- 각자 baseline 코드 리뷰
  - train loader의 drop_last
    - 통용적으로 사용
  - 시드 고정 함수 중요 (테스트를 하기 위해)
  - DataParallel == MultiGPU 사용할 때
  - AdamW 도 사용해보기, AdamP
  - multi head 보다 Separate Model로 나누어보기
  - 학습때 age regression 해보기
    - 10대 20대 30대 등으로 나눠서 최대한 학습 데이터 이용하기
  - EMA (Exponential Moving Average) 사용해보기
  - BatchNorm
  - Augmentation
    - RandomCrop 이 생각보다 좋음 (가로 세로 70, 80% 정도)
  - SwinTansformerV2 사용해보기

---

# 피어세션
- P-stage, 회고
- 피어세션 시간을 따로 두지않고 코어타임 내 전체 zoom 미팅

---

# 스페셜 피어세션
- 자기소개
- 각자 팀 해결 방법
  - 트릭의 요소가 있을 듯
  - 모델의 구성요소
  - 레이블 수정 방법
- 팀 이탈 이유?
- 멘토 사용 방법
  - 1대1 멘토링
  - 멘토님께 질문하는 방법
  - 슬랙 대화를 적극 활용

---

# 마스터 클래스 (김태진 마스터님)

- 대회 리뷰
  - 12조 
    - 대회 내용
      - Data 분석을 통해 얼굴 위치 확인
      - Retina Face를 활용하여 얼굴 Crop
      - 여러 모델 분석
      - K-Fold, F1 Loss 등 여러 기법을 적용
    - 협업 방법
      - Notion을 활용하여 활동 기록을 남김
      - VS Code Share 이용
  - 9조
    - 대회 내용
      - 3way model, single model
      - Data 분석
        - Data Imbalance
        - Data 경계값 제거
        - 데이터 품질 -> Noise 제거
          - Data Noise -> Face detection
          - Label Noise -> API 이용하여 전체 레이블 검사
      - Data Augmentation
        - Augmentation 관련 실험을 통해 데이터에 맞는 기법 적용
        - TTA
        - 작은 수의 레이블을 Augmentation (Cutmix 등)
      - Model Selection
      - training
        - Cutmix
        - Model Debugging
        - OOF (hard voting)
- 방향을 도식화하고 결과를 정리해보는 것이 중요함
- 결과가 중요한 것이 아니라 과정이 중요
  - 회고를 통해 앞으로 해야할 떄의 중요한 부분을 정확히 파악하는 것
- 문제들을 정확히 정의하는 것, 그에 따른 솔루션을 명확하게 정리하는 것이 중요
- 분석하여 나온 해결 방안들을 구현하거나 실행하는 실행력
  - 다양한 상상과 그를 이어가는 실행력
- 행동(모델 선정이나 전처리 등등)에 이유를 정확히 파악
- 학습 20 구현 30 문서 50
  - 문서화하고 행동의 이유와 설득하는 것 중요
- 대회에 특화된 테크닉 X, 테크닉 이해하고 실제로도 사용하는 것이 중요
- 코드 작성이 중요한 것이 아닌 Task에 의문점이나 생각들을 정리해보기

---

# 오피스아워 (최영선 조교님)

- 주제 : Image Classification using Azure Machine Learning - MLaaS(ML as a Service)
  - as a Service
- Azure Machine Learning
  - MS와의 연동성이 장점
  - GUI
  - Auto ML
    - workflow 간단 설명
    - 예시 

---

### 참고자료
- 부스트캠프 AI Tech 교육 자료