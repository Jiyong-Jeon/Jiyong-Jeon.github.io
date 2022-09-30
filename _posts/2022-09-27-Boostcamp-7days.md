---
title: Boostcamp 7days
date: 2022-09-27 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [2weeks, 7day]
math: true
---

# 7일차 학습 정리
<h3 data-toc-skip> PyTorch 모델 불러오기 </h3>

- model.save
  - 학습의 결과를 저장하기 위한 함수
  - 모델 아키텍쳐와 파라미터 저장
- checkpoints
  - 학습 중간 결과를 저장하여 최선의 결과를 선택
  - loss와 metric값을 지속적으로 확인 저장
- Transfer learning
  - 다른 데이터셋으로 만든 모델을 현제 데이터에 적용
  - 현재 DL에서는 가장 일반적인 학습 기법
  - Backbone architecture가 잘 학습된 모델에서 일부분만 변경하여 학습을 수행
  - TorchVision, HuggingFace(NLP)
  - Freezing
    - pretrained model을 활용시 모델의 일부분을 frozen 시킴

<h3 data-toc-skip> Monitoring tools for PyTorch </h3>

- Tensorboard
  - TensorFlow의 프로젝트로 만들어진 시각화 도구
  - 학습 그래프, metric, 학습 결과의 시각화 지원 (시각화 핵심 도구)
  - scalar, graph, histogram, image, mesh
- weight & biases (wandb)
  - 머신러닝 실험을 원활히 지원하기 위한 상용도구
  - 협업, code versioning, 실험 결과 기록 등 제공

<h3 data-toc-skip> Multi-GPU 학습 </h3>

- GPU vs Node
  - Node : 컴퓨터 ex. Single Node Multi GPU (한대의 컴퓨터에 여러대의 GPU)
- 병렬화의 두 가지 방법
  - **model parallel**
    - 대표적으로 alexnet (생각보다 예전부터 사용)
    - 병목, 파이프라인의 어려움 등으로 모델 병렬화는 고난이도 과제
  - **data parallel**
    - 데이터를 나눠 GPU에 할당 후 결과의 평균을 취하는 방법
    - minibatch 수식과 유사
    - 한번에 여러 GPU에서 수행 
    - GPU 사용 불균형 문제 발생, Batch 사이즈 감소 (한 GPU가 병목)
    - DistributedDataParallel
      - 각 CPU마다 process 를 생성하여 개발 GPU에 할당
      - 하나 개별적으로 평균을 연산

<h3 data-toc-skip> Hyperparameter Tuning </h3>

성능을 높이기 위한 방법
1. 모델 (많이 알려짐)
2. 데이터 + (데이터는 많을수록 좋다.)
3. Hyperparameter tuning
- hyperparameter
  - 모델 스스로 학습 하지 않는 값 (사람이 지정)
  - learning rate, 모델의 크기, optimizer 등
- 기본적인 방법
  - grad vs random (search)
    - 사진 비교 [grad vs random]
  - 최근에는 베이지안 기반 기법들
- Ray
  - Multi-node multi processing 지원 모듈
  - ML/DL의 병렬처리를 위해 개발
  - 현재의 분산병렬 ML/DL의 표준
  - Hyperparameter Search를 위한 다양한 모듈 제공

<h3 data-toc-skip> PyTorh Troubleshooting </h3>

- OOM (Out Of Memory)
  - 왜, 어디서 발생했는지 알기 어려움 (이전 상황의 파악도 어려움)
- Batch Size 줄이기 이외에 해결 방법
  - GPUUtil 사용
    - Nvidia-smi 처럼 GPU의 상태를 보여주는 모듈
    - iter마다 메모리가 늘어나는지 확인 가능
  - torch.cuda.empty_cache() 써보기
    - 사용되지 않는 GPU상 cache를 정리
    - 가용 메모리 확보 
  - trainning loop에 tensor로 축적되는 변수는 확인할 것
    - tensor로 처리된 변수는 GPU상에서 메모리 사용
    - loop 안에 연산에 있을 때 GPu에 computational graph 생성 (메모리 잠식)
    - 1-d tensor의 경우 python 기본 객체로 변환하여 처리!
    - 필요가 없어진 변수는 적절한 삭제가 필요! (del 명령어 적설히 사용하기)
  - 가능 batch 사이즈 실험해 보기
    - 사이즈 1로 해서 실험해 보기
  - torch.no_grad() 사용하기
    - backward pass 로 인해 쌓이는 메모리 해소
    - inference 시점 사용
- 예상치 못한 에러 메시지
  - 엄청 많음
  - 개인적으로 정리할 필요가 있음

---

# 기본 과제
- **Custom_model 제작** (1)
  - 난이도는 대체로 쉬웠음
  - 가이드에 따라 읽고 실습하는 부분이 많아 시간이 오래걸림

---

# 피어세션
- 학습내용 공유
  - 과제 관련 토의
  - 다음 주 부터는 학습 속도를 맞추기로 결정
- 팀 대회
  - 베이스코드 테스트
  - 데이터 카테고리 분류 방법 논의
- [회의록](https://night-eustoma-5f3.notion.site/9-27-20395f5f80e148debfeef3193a7e9545)
  
---
### 참고자료
- 부스트캠프 AI Tech 교육 자료