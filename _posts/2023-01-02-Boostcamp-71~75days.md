---
title: Boostcamp 71~75days
date: 2023-01-02 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [16weeks, 71day, 72day, 73day, 74day, 75day]
math: true

---

# 주간 학습 정리

---

# 피어세션
- P-stage
  - baseline을 통해 여러 실험들을 진행
  - 많은 모델을 사용해보고 실험결과를 기록하기
  - 앙상블 등 여러 기법들 적용해보기
    - 여러 기법을 적용해 볼수록 성능이 떨어짐..?
  - 결과를 확인해보면서 무엇이 문제인지 계속 토의
- 최종 프로젝트
  - 역할 분담은 어떻게 할 것 인가?
    - 프로젝트를 진행하며 유동적으로 담당자 두는 방식
    - PM은 스케줄 관리 정도?
    - 역할 분담보다 프로젝트 스케줄을 먼저 짜보자
      - 프로젝트에 필요한 요소들을 찾아봐야할듯
  - 다음주 까지 MMDetection3D 돌려보기
- 오프라인 계획 세우기

---

# 멘토링
- P-stage 대회 관련
  - 스코어의 한계
    - 문제정의가 제대로 되어있지 않은 것 같다.
    - EDA나 다른 방식으로 문제정의 부터
      - confusion을 이용해보자
    - 모델 변경에 너무 국한 되어있는 듯함
  - augmentation
    - 멘토님의 방식 : 데이터 셋에 맞는 augmentation 찾고 모델을 찾는 방식 이후 다른 기법들 적용
  - 스코어를 꼭 mIoU만 볼게아니라 다른 메트릭을 참고해봐도 좋을 듯
  - 작년의 경우 좋은 소타 모델을 찾는 것으로 좋은 성적을 냄
- 최종 프로젝트
  - 2D이미지만 사용해서 3D detection vs 2D이미지와 lidar 센서 멀티모달
  - edge : 자이버 활용
  - 데이터셋 수집 or 모델 변경(경량화)에 대한 pipeline도 구축해보는 것도 좋을 듯 (디테일 추가)
  - self-supervised learning
    - 관련 자료
  - optional
    - 자율주행에 대한 것에 multi task 추가?
    - 잘못 한 것들에 대한 신호를 주는 task도 좋아보임
  - 역할 분담에 대해서도 생각을 해봐야함
    - 모두가 다같이 진행을 할 것인지
    - 역할 분담 이후 주마다 세미나를 할 것인지?

---
# 두런두런 4회차
- 이력서
  - 보는 사람을 배려한 이력서
  - 좋은 이력서
    - 숫자가 있는 프로젝트 (성과)
    - 고민의 흔적이 있는 프로젝트
- 고민 상담소
- Engineering Carrer Framework
  - 프레임워크를 참고해서 삶의 지도에 미래를 추가할 수 있음
  - 자신의 강점을 어떻게 발현하고 더 개선할 것인지?
- 회사 찾기
  - 회사에 나를 맞추는 것이 아닌
  - 나와 회사의 교집합을 찾고 교집합을 통해 지원동기를 찾음
  - 산업 찾기
    - 좋아하는 것 사이에서 산업을 찾아보기
    - 산업의 매력? 유명 기업은? 왜 좋은지?
  - 찾은 것들을 기록하는 것이 중요!
- 두런두런 1~4회차하면서 회고, 후기 포스팅해보기
  - 뭘 배웠는가?
  - 어떤 영향을 끼쳤는가?

---
# 부캠 라디오

---

# 스페셜 피어세션
- 다른 트랙과의 피어세션
  - 트랙별 고충 공유
  - 트랙별 인기 스타? 열정을 따라가는법
  - 최종 프로젝트
    - 프로젝트? 어떤게 좋을까
    - 역할 분배에 대해서 
      - pier coding
      - 크게 분배를 하고 팀(2~3명)을 나누기
      - 모두가 해봐야 할것들은 다같이, 세부적으로 원하는 것들을 분배
- 같은 트랙 끼리 피어세션
  - 이력서
    - 수치
      - 과연 의미있는 수치인가?
      - 수치가 꼭 필요한 것인가?
      - 수치가 중요한 것이 아닌 거기에 담긴 의미
      - 수치가 없더라도 효과나 필요성에서 강조
  - 원하는 기업?
    - AI 클로바
    - CV가 잘 맞으면 CV 커리어를 쌓을만한 회사? 회사의 주력 부문? 흥미를 찾아보기
  - AI-stage
    - 모델
      - Beit 모델
        - 좋은 성능을 냈음
      - HRnet+FCN, Upernet, Eff, beit, swin
    - Augmentation
      - imblance한 object 붙이기
    - Pseudo labeling
      - 성능 향상에 많이 도움을 줌

---
# 마스터 클래스
- 대회 1~2등 솔루션 발표
- 협업 방식
  - github, slcak, slack huddle 활용, Notion
- 대회 준비
  - Streamlit 활용
    - Data Viewer
      - 이미지, 결과를 확인
    - Data Augmentation
      - Augmentation을 적용한 이미지를 눈으로 확인
  - ML flow
- 모델 선정
  - Mask2Former
  - Beit V2
- 대회 전략
  - Data Augmentation
    - Multi-scaling, Random Crop, Color jittering, Random horizontal Flip, PhotoMetricDistortion
  - K-Fold
- Ensemble
- Dense CRF
  - 작은 물체를 지우는 경향이 있었음
    - 앙상블 기법을 통해 작은물체를 살림
- Pseudo Labeling
  - 전체적으로 향상됌
- 학습 중 특이사항
  - validation set이 전체 dataset을 대표하지 못함
  - 학습 데이터에 mislabeling이 많음
- 대회의 문제점을 제대로 분석하고 문제를 하나씩 풀어가는 것이 중요
  - 여러 자료를 찾아보면서 해결

---
### 참고자료
- 부스트캠프 AI Tech 교육 자료