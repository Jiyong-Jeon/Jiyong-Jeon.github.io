---
title: Boostcamp 33days
date: 2022-11-07 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [8weeks, 33day]
math: true

---

# 33일차 학습 정리

<h3 data-toc-skip> AI 서비스 개발 기초 </h3>

- 강의 소개
  - AI 엔지니어가 되기 위한 기본 소양을 갖추기
  - 문제 정의에 대한 고민을 하는 사람
  - 라이브러리가 왜 만들어졌는지에 중점
- 추천 학습 방식
  - 강의는 1회만
  - 흐름 위주로 키워드를 필기하면서 수강
  - 왜?에 대한 고민해보기
  - 복습은 강의 자료를 최대한 활용 (큰 뻐대를 스스로 떠올려 보기)
  - 자신의 언어로 정리해보기

<h3 data-toc-skip> MLOps 개론 </h3>

- 모델 개발 프로세스(Research)
  - 문제정의 -> EDA -> Feature Engineering -> Train -> Predict
  - 고정된 데이터를 사용해 학습
- 모델 개발 프로세스(Production)
  - Real World, Production 환경에 모델을 배포
  - 문제정의 -> EDA -> Feature Engineering -> Train -> Predict -> Deploy
  - 모델의 결과값이 이상한 경우가 존재 (input, outlier 등)
  - 모델의 성능이 계속 변경
- 차이
  - ![Reserch와 Production 차이](/img/post/boostcamp_33days_img_1.png)
- MLOps
  - ML(Machine Learning) + Ops(Operations)
  - 머신러닝 엔지니어링 + 데이터 엔지니어링 + 클라우드 + 인프라
  - 목표
    - 머신러닝 모델 개발(ML Dev)과 머신러닝 모델 운영(Ops)에서 사용되는 문제, 반복을 최소화하고 비즈니스 가치를 창출하는 것
    - 빠른 기간 내에 가장 적은 위험을 부담하며 아이디어 단계부터 Production단계 까지 ML 프로젝트를 진행할 수 있도록 기술적 마찰을 줄이는 것
  - MLOps의 각 Component에서 해결하고 싶은 문제는 무엇이고 해결하기 위한 방법으로 어떤 방식을 활용할 수 있는지 학습
- MLOps Component
  - 머신 러닝 모델을 직접 운영하면서 신경써야하는 부분들
  - Server 인프라
    - 예상 트래픽, 서버 성능, 스케일, 서버 환경 등
  - GPU Infra
  - Infra
    - 클라우드(AWS, GCP, Azure, NCP 등)
    - 온 프레미스(회사나 대학원의 전산실에 서버를 직접 설치, NVIDIA 등)
  - Serving
    - Batch Serving
      - 많은 데이터를 일정 주기로 한꺼번에 예측
    - Online Serving 
      - 한번에 하나씩 실시가능로 예측
    - Cortex, BentoML, torch/serve, tensorflow/serving, seldon-core, kfserving, clipper
  - Experiment, Model Management
    - 모델 학습의 부산물 저장 (모델 Artifact, 이미지, 모델 메타 정보 등)
    - MLFlow (학습 기록을 자동으로 저장해줌)
  - Feature Store
    - 머신러닝 Feature(벡터를 미리)를 집계한 Feature 저장해두고 사용
    - FEAST 라이브러리 (https://feast.dev)
  - Data Validation
    - Data Drift, Model Drift, Concept Drift
    - TFDV(Tensorflow Data Validation) 라이브러리
    - AWS Deequ : Unit Test for data, Data Quality 측정
  - Continuous Training
    - Retrain
      - 새로운 데이터 생성, 일정 기간, Metric기반, 요청시에 재학습
  - Monitoring
    - 모델 지표, 인프라 성능 지표 등을 기록
  - AutoML
  - Practitioner Guide to MLOps 참고
  
<h3 data-toc-skip> Model Serving </h3>

- Serving
  - 머신러닝 모델을 개발하고, 현실 세계(앱, 웹)에서 사용할 수 있게 만드는 행위, 서비스화
  - 방식
    - Online Serving, Batch Serving, Edge Serving(IOT 등)
- Online Serving
  - Web Server Basic 소개
    - Server와 Client간의 Request, Response 예제
    - API(Application Programming Interface)
  - 요청(Requset)이 올 때마다 실시간으로 예측
  - 단일 데이터
  - 방식
    - 직접 API 웹 서버 개발 : Flask, Fast API 등
    - 클라우드 서비스 활용 : AWS의 SageMaker, GCP의 Vertex AI 등
    - Serving 라이브러리 활용 : Tensorflow Serving, Torch Serve, MLFlow, BentoML 등
  - 주어진 환경에 맞는 serving 방법을 찾기
  - Python 버전, 패키지 버전 등 Dependency가 중요
  - 지연 시간(Latency)를 최소화 해야함
    - Database 쿼리 시간, 모델 수행 시간
  - 결과 값에 대한 보정이 필요할 때도 있음
- Batch Serving
  - Workflow Scheduler 등 주기적으로 학습을 하거나 예측
  - Batch 단위 데이터
  - Online Serving 보다 구현이 간단, Latency가 문제가 되지 않음
  - 실시간 활용은 불가능
  - Workflow Scheduler
    - Airflow, Cron Job
- 문제 상황에 맞게 적절한 Serving 방법을 찾는것이 중요

<h3 data-toc-skip> 머신러닝 프로젝트 라이프 사이클 </h3>

- 문제 정의
  - 특정 현상을 파악하고 그 현상에 있는 문제를 정의하는 과정 (본질을 파악하는 과정)
  - 문제를 잘 풀기 위해선 문제 정의가 매우 중요함!
1. 현상 파악
2. 구체적인 문제 정의
   - 문제 상황, 원인, 해결 방안
3. 프로젝트 설계
   - 문제정의 -> 최적화할 Metric선택 -> 데이터 수집(레이블 확인) -> 모델 개발 -> 예측결과를 토대로 Error Analysis -> 반복
   - 머신러닝 문제 타당성 확인
     - 비즈니스적 가치가 있는가?, 패턴이 있는가? 있으면 복잡한 패턴, 목적 함수, 데이터 존재 여부, 반복성
   - 목표 설정, 지표 설정
     - Goal : 프로젝트의 일반적인 목적, 큰 목적
     - Objectives : 목적을 달성하기 위한 세부 단계의 목표(구체적인 목적)
     - Multi Objectives Optimizer
       - Objective가 여러개인 경우 분리하는 것이 좋음
   - 제약 조건 (Constraint & Risk)
     - 일정, 예산, 관련된 사람
     - Privacy, 기술적 제약, 윤리적 이슈
   - 베이스라인, 프로토타입
     - 모델이 더 좋아졌다고 판단할 수 있는 Baseline 필요
   - Metric Evaluation
     - 앞선 문제들을 해결할 경우 어떤 지표가 좋아질까?
     - 작게는 모델의 성능 지표(RMSE), 크게는 비즈니스의 지표
     - 행동의 성과를 파악하기 위해 지표를 잘 정의해야함
4. Action(모델 개발 후 배포 & 모니터링)
   - 앞서 정의한 지표가 어떻게 변하는지 파악
5. 추가 원인 분석
   
- 비즈니스 모델
  - 비즈니스 모델 파악하기
    - 회사가 어떤 서비스, 가치를 제공하고 있는가?
  - 데이터 활용 부분 (Input)
    - 데이터가 존재하는가? 무엇을 할 수 있는가? 등등
  - 모델을 활용 부분 (Output)

---

# level2 피어세션
- Lv1 대회 회고
  - Lv2에 참고할 것
- Lv2 대회 준비 계획
- 경진대회 어떻게 할지
- 국방 AI 대회 참가 준비
  - Change Detection 주제
    - Baseline 구축하기

---

# 피어세션
- 강의 내용 공유
  - 스페셜 미션 계획
  - Further Question 풀이 공유
- 멘토링 주제 선정
  - 각자 관심이 있는 주제를 이야기해봄
- [회의록](https://night-eustoma-5f3.notion.site/11-7-3f64e759663645fd9e242040781ac5a6)

---

# 주말 간 특별한일

- 2022 Animal Datathon 대회 본선
  - 과제1 : 축사 내 돼지의 자세분류
    - 레이블이 주어지지 않은 돼지 이미지의 자세 분류
  - Unsupervised, self-supervised Learning 기법 구현
  - 레이블링을 직접하여 Supervised Learning 과 Self-supervised Learning 비교
  - PCA+K-mean를 활용한 Unsupervised Learning 시도
  - Pretrained 모델 사용 금지
- 국방 AI 준비

---

### 참고자료
- 부스트캠프 AI Tech 교육 자료