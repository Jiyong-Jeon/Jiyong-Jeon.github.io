---
title: Boostcamp 69~70days
date: 2022-12-26 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [15weeks, 69day, 70day]
math: true

---

# 69~70일차 학습 정리

---

# 피어세션
  - P-stage
    - EDA 부터 차근차근히 해보기
      - 이전 피드백에 EDA에 견해까지 포함하는게 좋다하여 분석내용까지 추가
    - Baseline 작성
      - MMsegmentation vs SMP
    - 협업 방식을 더 체계적으로
---

# 이력서 피드백 세션
- 이력서 피드백 세션 노션 링크 (개인정보로 인해 닫음)
  - 이력서를 작성하고 Notion을 이용하여 공유
  - 댓글을 달아서 팀원들간에 서로 피드백 해주기
  - 피드백 정리

---

# 오피스 아워 (오휘건 조교님)
- mmseg 이용해 보기
- mmseg training 흐름
  - config
    - model, dataloader 등 학습시 필요한 설정을 모아둠
    - fromfile메서드가 .py파일을 파싱하여 순서대로 정의 된 부분을 가져옴
      - 파싱 예시
  - Registry
    - Object 생성 과정
  - Segmentor
    - forward 등 함수가 정의되어있는 class
    - backbone, decode_head(+loss function)
  - Dataset
    - data pipeline
  - train_segmentor function
    - 학습에 필요한 요소들을 만들고 학습을 시작하는 함수
      - dataset을 가지고 loader 만들기
      - optimizer, runner, running config, hook 등
- P-stage 학습 예제 (순서)
  1. dataset 구현
     - CustomLoadAnnotation (mmseg format이 아니기 떄문에)
  2. Model config 설정
  3. training 시나리오에 따라 학습
- Segmenation 이 생성모델에서 어떤식으로 사용되는지

---

# 스페셜 피어세션 (Boost up)
- p-stage 전략 공유?
- 최종 프로젝트를 진행할 때 유의할점
- 어떤 프로젝트를 진행할지 공유
- 팀 별 소통의 문제점, 해결방안 토의

---
### 참고자료
- 부스트캠프 AI Tech 교육 자료