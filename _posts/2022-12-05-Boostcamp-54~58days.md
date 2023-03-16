---
title: Boostcamp 54~58days
date: 2022-12-05 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [12weeks, 54day, 55day, 56day, 57day, 58day]
math: true

---

# 54~58일차 학습 정리

<h3 data-toc-skip> 데이터 제작의 중요성 </h3>

- Software 1.0 vs Software 2.0
- Software 1.0
  - 문제정의
  - 큰 문제를 작은 문제들의 집합으로 분해
  - 개별 문제 별로 알고리즘 설계
  - 솔루션들을 합쳐 하나의 시스템으로
  - Visual Recognitnion Task
    - HOG Det, DPM ..
    - 사람이 특징을 추출하고 ML 판단
    - 2.0은 사람이 개입하지 않음
  - 어떤 연산을 할지 사람이 고민하여 정하는 것
- Software 2.0 (Deep learning)
  - 뉴럴넷의 구조에 의해 검색 영역이 정해짐
  - 이후 최적화를 통해 목적에 적합한 연산을 찾아냄
  - 데이터와 최적화 방법에 의해 경로와 목적지가 정해짐
- Lifecycle of an AI Project
  - 서비스향 AI 모델 개발 과정 단계
    - Project Setup
      - 모델 요구사항 확정
    - Data Preparation
      - 데이터셋 준비
    - Model Training
      - 모델 학습 및 디버깅
    - Deploying
      - 설치 및 유지보수
  - Data-Centric
    - 데이터만 수정하여 모델 성능 끌어올리기
  - Model-Centric
    - 데이터는 고정시키고 모델 성능 끌어올리기
- Data-related task
  - 데이터를 어떻게 하면 좋을지에 대해서 알려져 있지 않다.
  - 데이터 라벨링 작업은 생각보다 어렵다
    - 라벨링 노이즈를 상쇄할 정도로 깨끗한 라벨링 데이터가 필요
    - 골고루(balance), 일정하게(clean) 라벨링된 데이터가 필요
  - 데이터 불균형을 바로잡기 어렵다
    - 해당 태스크에 대한 경험치가 잘 쌓여야한다.
- Data Engine / Flywheel
  - Software 2.0 IDE, 필요한 기능들(데이터 관점)
    - 데이터셋 시각화
    - 데이터 라벨링
    - 데이터셋 정제
    - 데이터셋 선별

<h3 data-toc-skip> OCR Technology & Service </h3>

- OCR(Optical Character Recognition) Tech
  - 글자 영역 찾기 + 영역 내 글자 인식 = OCR
  - CV + NLP 교집합의 영역
  - Serializer
    - OCR 결과값을 자연어 처리하기 편하게 일렬로 정렬하는 모듈
  - Text Parser
    - BIO 태깅을 활용한 개체명 인식 : 문장에서 기 정의된 개체에 대한 값 추출
    - BIO : Begin/Inside/Outside
- OCR Service
  - Text Extractor
    - Copy & Paste
    - \+ Search, \+ Matching, \+ 번역
  - Key-Value Extractor
    - ex. 신용카드(카드번호, 유효기간), 신분증, 수기 입력 대체

<h3 data-toc-skip> Text Detection </h3>

- 일반 객체 영역 검출 vs 글자 영역 검출
  - 객체들의 특징들을 알아야함
    - 매우 높은 밀도, 극단적 종횡비, 특이 모양(구겨진, 휘어진, 세로 쓰기), 모호한 객체 영역, 크기 편차
  - 글자 영역 표현법
    - 직사각형, 직사각형+각도, 사각형, 다각형
- Regression-based
  - 이미지를 입력받아 글자 영역 표현값들을 바로 출력으로
- Segmentation-based
  - 이미지를 입력받아 글자 영역 표현값들에 사용되는 화소 단위 정보를 뽑고, 후처리를 통해 최종 글자 영역 표현 값들을 확보
- hybrid
  - Regression-based + Segmentation-based
- Character-based Method vs Word-based Method
- ESAT 모델 소개
  - 모델 구조
    - 크게보면 U-net 구조
    - Feature extractor stem(backbone)
      - PVANet, VGGNet, ResNet50
    - Feature merging branch
      - Unpool로 크리글 맞추고 Concat
    - Output
      - H/4 * W/4 * C maps
      - Score Map
        - 글자 영역 중심에 해당하는지
      - Geometry Map
        - 어떤 화소가 글자 영역이라면 해당 Bounding box의 위치는 어디인지
  - Inference
    - Step1. Score Map 이진화
    - Step2. 사각형 좌표값 복원
    - Step3. NMS
      - Standard NMS
        - 복잡도가 $O(N^2)$로 Dense prediction 상황에 부적합
      - Locality-Award NMS
        - 인접한 픽셀에서 예측한 Bounding box들은 같은 text instance일 가능성이 높음
  - Training
    - Loss = Score map loss + Geometry map loss


<h3 data-toc-skip> Annotation Guide </h3>

- 가이드라인
  - 좋은 데이터를 확보하기 위한 과정을 정리해 놓은 문서
    - 좋은 데이터 = 골고루 모여있는(Raw Data) + 일정하게 라벨링된 (Ground Truth)
  - 라벨링에 관한 이야기만 다룸
  - 라벨링할 사람들에게 전달할 것
  - 구성
    - 학습 목적
      - 목적에 맞게 일관되게
      - 데이터의 일관성
    - 특이 케이스
      - 가능한 모든 특이케이스가 다 고려해야함
    - 단순함
    - 명확함
- 데이터 셋 제작 파이프라인
  - 서비스 요구사항 -> 제작 목적 설정 -> **가이드 라인 제작** -> RawImage 수집 -> 어노테이션(라벨링)
  - RawImage 수집
    - 크롤링
      - 좋은 키워드 선정, 필터링
    - 클라우드 소싱
- 가이드라인 제작과정
  - 가이드 작성 -> 가이드 교육 -> 라벨링 -> 라벨링 검수(라벨링 노이즈 관점) -> 데이터 검수(데이터 분포와 라벨링 노이즈 관점)
  - 가이드 라인 versioning 중요
  - 용어
    - ![용어 정리](/img/post/boostcamp_54days_img_2.png)
  - Annotation규칙
  - 최종 포맷
  - 일관성 있게 작성이 되어야 함
  - 가이드 라인 작성시 우선순위가 필요하다
    - 학습 관점
  - 구축 과정 감수
    - 감독자 전수검사, peer check, 다수결
  - 초기에 소량씩 완성본 받아서 품질을 확인 
  - 작업자 QnA 활용
  - 추가 수정을 위한 비용과 시간이 크다면 어느정도 포기

<h3 data-toc-skip> 성능평가 개요 </h3>

- 성능평가 (일반화 성능)
  - 새로운 데이터가 들어왔을 때 얼마나 잘 작동하는가? 
- 추가 분석 방법
  - Confusion Matrix, Recall/Precision
- 정량평가의 기준에 따라 점수가 달라진다.
- 글자 검출 모델 평가
  - 1. 테스트 이미지에 대해 결과값을 뽑는다.
  - 2. 예측 결과와 정답 간 매칭/스코어링 과정을 거쳐 평가
    - 두 영역간의 매칭 판단 방법(매칭 행렬 계산) + 매칭 행렬에서 유사도 수치 계산 방법(유사도 계산)
- 두 영역간의 매칭 판단 방법(매칭 행렬 계산)
  - IoU
  - Area Recall / Area Precision
  - One to One Match / One to Many Match / Many to One Match
- 실제 사용되는 방식
  - DetEval
    - 모든 정답 영역, 예측 영역 간의 매칭 정보를 area recall/area precision 둘 다 계산 (관계 하나마다 두개의 수치 확보)
    - Binary scoring
      - 셀 중에 area recall >= 0.8 and area precision >= 0.4 조건을 충족하면 1 아니면 0 값으로 관계 행렬값을 바꿈
    - 이진 행렬 값을 활용하여 One to one, one to many, many to one 구분
  - IoU
    - One to One Match만 허용
  - TIoU (Tightness-aware IoU)
    - 부족하거나 초과된 영역 크기에 비례하여 IoU점수에 대해 Penalty 부여
  - CLEval
    - 얼마나 많은 글자를 맞추고 틀렸냐를 가지고 평가
    - Character-Level Evaluation
    - PCC(Pseudo Chracter Centers)
      - 글자의 중심을 계산
    - CorrectNum, GranualPenalty, TotalNum으로 Recall / Precision 계산
- 성능 평가에 따라 목적과 목표가 달라짐

<h3 data-toc-skip> Annotation 도구 소개 </h3>

- 양질의 데이터를 확보하려면 필요한 요소
  - 사람, Process, Tool
- CV 데이터 제작 오픈소스
  - LabelMe
    - 장점
      - 설치가 용이하다
      - python으로 작성되어 추가적인 기능 추가 가능
    - 단점
      - 공동작업이 불가능
      - 속성을 부여할 수 없음
  - CVAT (Computer Vision Annotation Tool)
    - 장점
      - 다양한 Annotation 지원
      - Automatic annotation 기능으로, 빠른 annotation 가능
      - 온라인에서 바로 사용하거나, 오픈소스도 제공되어 on-premise로 설치하여 이용가능
      - Multi-user, Assignee, Reviewer 기능 제공
    - 단점
      - Model inference 가 굉장히 느림
      - 속성을 부여하기 까다로움
  - Hasty Labeling Tool
    - 웹에서 데이터 제작/모델 학습/서빙/모니터링 까지 모두 제공
    - 장점
      - semi-automated annotation 기능을 지원
      - cloud storage 활용 가능 (유로)
      - Multi-user, Assignee, Reviewer 기능 제공
    - 단점
      - free credit을 다 소진한 이후에는 과금을 해야함
      - annotator가 수동으로 이미지마다 review state로 변경해 줘야함
      - annotation 도구에 대한 커스터마이징 불가 (Hasty 플랫폼에 강하게 연결되어 있음)
- Upstage annotation tool 설명

<h3 data-toc-skip> Bag of Tricks </h3>

- Synthetic Data
  - 성능 향상에 있어 가장 중요한 것이 Data이지만 Real Data를 확보는 어려운 일
    - Real data 확보 = public dataset + 직접 만들기
  - 장점
    - Real Data에 대한 부담을 덜어준다.
    - 비용이 적게 든다.
    - 개인정보나 라이센스에 관한 제약으로부터 자유롭다.
    - 세밀한 수준의 annotation도 쉽게 얻을 수 있다.
  - Synth Text
    - 800K dataset + 글자 합성 코드 제공
    - 이미지 Data + 글자 Data
    - Depth Estimation
      - 적절한 위치에만, 포면 모양에 맞춰서 글자를 합성
  - Synth Text 3D
    - 3D 가상 세계를 이용한 텍스트 이미지 합성
  - Unreal Text
    - 3D Virtual Engine을 이용 (개선된 Viewfinding)
  - Pretrained
    - Pretrained(Imagenet) -> Pretrained(Synthetic Data) -> fine-tuning(target data)
- Data Augmentation
  - Image Data Augmentation
    - Geometric Transformation
      - filp, resize, rotate...
      - Rule 1. Positive ratio 보장
        - 글자와 멀리있는 배경에서 hard negative sampling 이 잘 되지 않는다. 
          - 해결법: hard negative sample mining
      - Rule 2. 개체 잘림 방지
        - 밀집 된 곳에서는 sampling이 잘 되지 않는다.
          - 해결법: 룰을 완화한다. (최소 하나의 객체는 잘리지 않아야한다로 변경)
    - Style Transformation
      - colorjitter...
    - Other Transformation
      - Cutout, grip ...
  - 실전에서는 상황에 따라 크게 다름
- Large Scale Variation
  - Multi-Scale Training
    - 다양한 크기로 바꿔가면서 입력해준다.
    - SNIP - Scale Normalization for Image Pyramid
  - Multi-scale inference
    - Adaptive Scaling
      - 이미지를 2차례 입력 : 글자의 위치와 크기를 대략적으로 예측하고 그 결과를 기반으로 재구성한 이미지를 다시 입력하여 최종 결과를 얻는 방식
      - Canonical KnapSack
        - 배경영역에 대한 계산을 하지 않아 경제적이다.
        - 글자들의 크기가 적정 크기로 통일되어 scale variation으로 인한 성능 저하가 없다.

---

# 피어세션
- 기업연계 프로젝트 신청 여부 확인
- annotation tools 사용 경험 공유
- 데이터 제작 프로젝트 계획

---

# 기업연계 프로젝트 티타임 미팅
- 기업연계 프로젝트 설명
- 노타 - Semantic Segmentation 경량 모델링
- 파인더스에이아이 - Object detection in retail
- 누비랩
- 업스테이지


---

# 오피스 아워
- 이번 실습 개요
  - OCR 엔진의 성능을 향상시키기 위한 학습 데이터 구축 경험
- Textbox Labeling 가이드
  - 이미지 상에 존재하는 글자에 박스를 그리고 글자를 전사 하는 작업
  - ![용어 정리](/img/post/boostcamp_54days_img_1.png)
  - 라벨링 방법
    - 폐기(Hold) 대상 구분
    - 제외 영역 구분 (번짐, 가려짐, 잘림, 밀도 등등)
    - 텍스트 박스 그리는 방법
    - 텍스트 박스 분리 기준
    - 텍스트 전사 방법
      - \<UNK> 이란
      - 특수문자 기준
    - 텍스트 진행 방향
    - 태그
      - 언어 태그 (문자 쳬게 표시)
      - 워드 태그(반전, 비친글자, 가려짐, 손글씨, 취소선, 음각/양각, 디지털 글자, 도장, 로고, 워터마크, )
      - 이미지 태그 (노이즈, 문서, 손글씨, 아풋포커스, 노트)
      - 태그는 추가할 수 있지만
  - 라벨링 과정
    - 이미지 확인 후, 폐기 결정
    - 읽을 수 없는 글자에 대해서 제외 영역으로 주석
    - 읽을 수 있는 모든 글자에 대해 텍스트박스를 그리고 텍스트 전사
    - 가로/세로쓰기, 태그 항목 추가
- UFO(Upstage Format for OCR) 변환 코드 가이드
  - 코드 설명

---

# 오피스 아워
- 베이스라인 코드 해설

---
### 참고자료
- 부스트캠프 AI Tech 교육 자료