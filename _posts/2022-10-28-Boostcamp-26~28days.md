---
title: Boostcamp 26~28days
date: 2022-10-28 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [6weeks, 26day, 27day, 28day]
math: true

---
# 26~28일차 P-stage

<h3 data-toc-skip> EDA </h3>

- Dataset 분석
  - 데이터 라벨 분석
  - 데이터 불균형 확인
  - 데이터 시각화
- PCA
  - RGB값을 활용하여 PCA 분석
  - 주성분을 활용하여 유의미한 분리 상황을 파악하지 못함
  - 0, 19 성분에서 미세하게 분리

<h3 data-toc-skip> Baseline code 분석 및 Custom </h3>

- 미션 풀이
  - 미션 1 ~ 6을 기반으로 나만의 baseline code 생성
  - 제공된 baseline code와 나만의 baseline code 비교
- Baseline code 분석
  - line by line 분석으로 python project 이해
  - python project -> juypter notebook으로 코드 변경
    - 실험 환경을 세세하게 하기 위해  
- Custom
  - 데이터 셋 Custom
    - Augmentation 적용
  - Pretrained 모델 Custom
    - VIT, ResneXt 모델 적용
    - Multi label head model
  - 원활한 실험 환경 변경을 위한 Config 클래스
  - 그 외, Optimizer, Schduler, loss 등 Custom
- 아직 해야할 일들이 많음


---

# 멘토링
- 서버 사용 시 유용한 것들
  - docker 기본
  - tmux 사용방법
- P-stage
  - PCA 분석방법
  - 팀 전략 피드백

---

# 피어세션
- P-stage
  - EDA 분석
  - 개인 서버 환경 설정
  - Baseline 코드분석
    - 각자 이해하고 line by line 분석 내용 공유
  - Baseline custom
    - 각자 방식대로 basecode 수정 후 공유
    - 잘한 것 과 잘못된 것을 공유하고 좋은 방향으로 baseline 수정
  - 성능 향상 전략 공유
- 피어세션 시간을 따로 두지않고 코어타임 내 전체 zoom 미팅
- [26일 회의록](https://night-eustoma-5f3.notion.site/10-26-7063980e17954b218b1bd25423424542)
- [27일 회의록](https://night-eustoma-5f3.notion.site/10-27-19a7d032be854f38b61c22b3b6fbea26)
- [28일 회의록](https://night-eustoma-5f3.notion.site/10-28-7583a76ae02748b388862ecf7487543b)

---

# 마스터 클래스 (김태진 마스터님)

- Stage 설계의 의도
  - U stage 복습 및 확장
  - 시행착오를 겪으며 많은 걸 시도해야함
  - 본인의 성장이 최우선
- P-stage 에서 해야할 것
  - Classification
    - 분류문제에도 다양함이 존재
      - Coarse-grained classification
        - 종이 다름 (구분이 명확함)
      - Fine-grained classification
        - 같은 종에 미세한 차이
    - 실제 데이터는 상당히 추상적
      - 문제 정의(Problem Definition)를 명확하게
  - Communication 중요
- 취업 준비?
  - DS, ML Engineer, Data Engineer 등 직군의 구별이 중요
  - 목표에 도달하기까지의 과정을 명확하게 설명하는 것이 중요
- 기업과 스타트업의 차이..?

---

# 오피스아워 (김보찬 조교님)

- P-stage Baseline 코드 설명
  - Baseline 활용 방법 예제
- python project vs jupyter
  - python project의 장점
    - ide 기능
    - 파일 구조화 -> 확장성, 재사용성, 가독성
    - CLI
- 목표
  - 코드 구조를 이해하고 좋은 구조로 기능을 확장시켜 나가는 능력
  - 좋은 코드의 구조를 이해하는 능력
  - 기존에 운영되던 레거시 코드의 문제점을 좋은 구조로 리팩토링 하는 능력


---

### 참고자료
- 부스트캠프 AI Tech 교육 자료