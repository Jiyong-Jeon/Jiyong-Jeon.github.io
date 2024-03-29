---
title: Boostcamp 3days
date: 2022-09-21 19:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [1weeks, 3day]
math: true
---

# 3일차 학습 정리
---
<h3 data-toc-skip> 베이즈 통계학 </h3>

- **조건부확률**
  - 사건 B가 일어난 상황에서 사건 A가 발생할 확률
  - $$ P(A\cap B) = P(B)P(A|B)$$
- **베이즈 정리**
  - 조건부확률을 이용하여 정보를 갱신하는 방법 (베이즈 정리 유도)
  - 예제 사진. D = 데이터, theta = 모수
  - 조건부 확률의 시각화 : confusion matrix
    - ![confusion matrix](/img/post/boostcamp_3days_img_1.png)
  - 조건부 확률은 유용한 통계적 해석을 제공
    - but, 인과관계(causality)를 추론할 때 함부로 사용해서는 안됨
    - 인과관계는 데이터 분포의 변화에 강건한 예측모형을 만들 때 필요
    - 인과관계를 알아내기 위해서는 중첩요인(confounding factor)의 효과를 제거하고 원인에 해당하는 변수만 계산

<h3 data-toc-skip> CNN 첫걸음 </h3>

- **convolution 연산**
  - 커널(kernel)을 입력벡터 상에서 움직여 가면서 선형모델과 합성함수가 적용되는 구조
  - 공통된 커널을 사용 (공통 가중치)
  - 수학적인 의미 : 신호를 커널을 이용해 국소적으로 증폭 또는 감소 시켜 정보를 추출 또는 필터링 하는 것
  - 채널이 여러개인 2차원 입력의 경우 2차원 Convolution을 채널 개수 만큼 적용
- **convolution 역전파**
  - 커널이 모든 입력데이터에 공통으로 적용되기 때문에 역전파를 계산할 때도 convolution 연산이 나옴

<h3 data-toc-skip> RNN 첫걸음 </h3>

- **시퀀스 데이터**
  - 소리, 문자열, 주가 등 시계열 데이터 (시간 순서에 따라 나열된)
  - 조건부확률을 이용하여 시퀀스의 정보를 다룰수 있음
  - 길이가 가변적인 데이터를 다룰 모델이 필요
    - 잠재변수를 신경망을 통해 반복 사용하여 시퀀스 데이터 패턴을 학습하는 모델 => RNN
- **RNN**
  - 이전 순서의 잠재변수와 현재의 입력을 활용하여 모델링
  - 역전파는 잠재변수의 연결그래프에 따라 순차적으로 계산
    - Backpropagation Through Time (BPTT) : RNN의 역전파 방법
      - 시퀀스의 길이가 길어질 수록 계산이 불안정 해짐 (기울기 소실)(과거정보 유실)
      - truncated BPTT : 길이를 끊는 방법
      - 길이가 긴 시퀀스를 처리하기위해 LSTM과 GRU가 등장

---
# 일반과제
- 파이썬을 이용한 간단한 문제

---
# 피어세션
- 피어세션 진행 주제 선정 회의 (논문리뷰, 대회참가 등등)
- 일반 과제 코드 리뷰
  - 각자 해결 방법을 설명 하고 코맨트를 주고 받음
- [회의록](https://night-eustoma-5f3.notion.site/9-21-fe7f8c74f631409cb20d1910e8da963a)
  
---
### 참고자료
- 부스트캠프 AI Tech 교육 자료