---
title: Boostcamp 64~68days
date: 2022-12-19 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [14weeks, 64day, 65day, 66day, 67day, 68day]
math: true

---

# 64~68일차 학습 정리

<h3 data-toc-skip> Semantic Segmentation </h3>

- 픽셀 단위 classification
  - Instance segmentation : 탐지된 인스턴스끼리 따로 분류
- 활용 분야
  - 자율 주행, 의료 등

<h3 data-toc-skip> P-stage Competition Overview </h3>

- coco format
  - info : dataset에 대한 high-level정보가 담김
  - lisense
  - images
  - categories
  - segmentation : 각 class 에 해당되는 pixel의 x,y좌표들이 포함
- Dataloader
  - image : (batch, 3, height, width)
  - label : (batch, height, width)
  - 필요 인자 : data_dir, mode(train, test), transform
- EDA
  - 11개의 클래스
  - 핵심 가설 설명
- 평가 : mIoU
- Baseline 설명

<h3 data-toc-skip> Segmentation FCN </h3>

- 요약
  - VGG 네트워크 백본을 사용
  - VGG 네트워크의 FC Layer를 Convolution layer로 대체
  - Transpose Convolution을 이용해서 pixel wise prediction 수행
- Backbone VGG
  - 백본이 VGG라면 다른 pretrained 모델도 사용가능
- Convolution Layer
  - 각 픽셀의 위치정보를 해치지 않음
  - 임의의 입력 크기에 모두 작동함
- Transpose Convolution
  - Upsampling == Deconvolution == Transposed Convolution
  - Transpose 라고 불리는 이유
  - 학습이 가능한 Weight임
  - 줄어든 이미지를 다시 키우는 Conv
- FCN 모델 구조 설명
  - 5개의 block 이후 Transpose conv
  - upsampling 과정에서 단계적 upsample 구조
- 평가지표
  - pixel accuracy
  - Mean IoU
- FC6 에 7x7 Conv를 사용하게 되면 발생하는 문제
  - Output 이미지의 크기가 달라짐
  - 처음부터 padding을 사용해 이미지를 키워서 학습하고 이후 crop하여 이미지크기를 맞춤


<h3 data-toc-skip> Sematic segmentation 대회에서 해봐야할 방법들 </h3>

- Library (segmentation_models_pytorch, mmSeg)
  - 모델 불러오기
- 실험 해봐야할 사항들
  - 주의사항
    - 디버깅 모드 
      - 실험 환경이 잘 설정되었는지 체크하기 위한 과정
      - 데이터의 일부를 샘플링하거나 1~2에폭만 돌려서 코드가 잘 돌아가는지 확인
    - 시드 고정
    - 실험 기록
      - Network종류, Augmenation, hyperparameter등 성능에 영향을 주는 조건을 기록
    - 실험은 한 번에 하나씩!
      - 하나의 조건만 변경해가며 실험
    - 팀원마다 역할 분배가 중요
  - Validation
    - 제출을 하지 않더라도 성능을 평가할 수 있음
    - Public 리더보드의 성능에 오버피팅되지 않도록 함
    - Hold out (8:2 분리)
    - K-Fold
      - Stratified K-Fold
      - Group K-Fold
  - Augmentation - Albumentation
    - 도메인에 맞는 Augmentation 기법 필요
    - Cutout, Gridmask, MixUp, Cutmix, snapMix, CropNonEmptyMaskIfExists
  - SOTA Model(HRNet)
    - 무조건 SOTA가 좋은건 아님, 도메인에 맞는지 확인이 필요
  - Scheduler
    - CosineAnnelaingLR, ReduceLROnPlateau
    - Gradual Warmup
  - Hyperparameter Tuning
    - batch size
      - Gradient accumulation (Grad를 모아서 한번에 업데이트)
  - Optimizer / loss
    - Compound Loss 계열 (imbalanced segmentation task에 강인함)

- 대회에서 주로 사용되는 기법들
  - Ensemble
    - 5-Flod ensemble
    - epoch Ensemble
    - SWA (Stochastic Weight Averaging)
      - 일정 주기마다 weight를 평균 내는 방법
      - 일반화 성능을 높이기 좋음
    - Seed Ensemble
    - Resize Ensemble
    - TTA
      - TTA Library - ttach
  - Pseudo Labeling
    - test 데이터셋에 대한 예측을 진행후 Confidence score가 높은 것을 골라서 학습에 사용
  - 외부데이터 활용 (캠프 대회에는 불가능)
  - Classification 결과를 활용하는 방법
  - 최근 딥러닝 이미지 대회 Trend
    - FP16, 실험 간소화(이미지 크기줄이기, 샘플링), 가벼운 모델 활용
    - 이미지가 크다면
      - resize, sliding window
  - 라벨에 Noise가 있는 경우
    - Label Smoothing
    - Pseudo-labeling을 활용한 Label Preprocessing
- Monitoring Tool
  - WandB
    - inference 결과를 Web에서 사용가능

<h3 data-toc-skip> FCN의 한계를 극복한 모델들 </h3>

- FCN의 한계점
  - 객체의 크기가 크거나 작은 경우 예측을 잘 하지 못함
  - Object의 디테일한 모습이 사라지는 문제
- Decoder를 개선한 모델
  - DeconvNet
    - Decoder를 Encoder와 대칭으로 만듬
    - Unpoolling
      - pooling시 지워진 경계에 정보를 기록했다가 복원
    - Deconvolution (Transpose Convolution)
      - 안의 정보를 복원
  - SegNet
    - Realtime에서 Semantic Seg를 수행하기 위함
      - 특히 자율주행에서 많이 사용
    - DeconvNet과의 모델 구조 차이 확인 (속도 관점)
      - FC layer를 줄여 속도 개선
- Skip Connection을 적용한 모델
  - Skip connect
    - 이전 layer의 output을 일부 layer를 건너 뛴 후의 layer에 입력으로 제공
    - Dense : 블럭 이전의 모든 정보를 건내주는 방식
  - FC DenseNet
  - Unet - 이후에 따로
- Receptive Field를 확장시킨 모델
  - Receptive Field
    - 뉴런이 얼마만큼의 영역을 바라보고 있는지에 대한 정보/영역
    - Conv->Maxpooling->conv 만으로도 효율적으로 Receptive field를 넓힐 수 있음
      - Resolution 측면에서는 low feature resolution을 가지는 문제점 발생
  - DeepLab v1
    - Dilated Convoultion & downsampling
      - Receptive field 넓히고, 파라미터 수 줄임
      - high resolution (이미지 크기를 적게 줄임)
    - Up Sampling - Bilinear Interpolation
    - Dense CRF(Conditional Random Field)(a.k.a Fully-Connected CRF)
      - CRF
        - 유사한 색상의 픽셀이 가까이 위치하면 같은 범주에 속하게
        - 모든 클래스에 대해 여러번 적용 후 가장 높은 확률을 갖는 클래스 선택
        - 디테일한 모습이 살아남
  - DilatedNet
    - Deeplab v1과의 구조 차이 비교
      - 좀더 효율적으로 Dilated conv를 사용하려함
  - DeepLab v2
    - vs. DeepLab
      - conv에서 3x3 maxpool layer가 삭제됨
      - fc6, fc7, fc8 layer가 추가됨
      - ResNet-101 구조 사용
  - PSPNet
    - 도입 배경
      - Mismatched Relationship : 객체들 간의 관계를 이해하지 못함
      - Confusion Categories : 카테고리를 혼돈함
      - Inconspicuous Classes : 객체가 작아서 예측하지 못함
    - 아키텍처
      - Pyramid Pooling Module
        - feature map에 average pooling을 적용하여 sub-region을 생성
        - sub-region 각각에 conv 진행, channel이 1인 feature map 생성
        - feature map 과 pyramid pooling module을 upsampling한 output을 서로 concat
  - DeepLab v3
    - ASPP Module
      - Multi-Size upscale
  - DeepLab v3+
    - Encoder-Decoder 구조: Encoder에서 spatial dimension의 축소로 손실된 정보를 decoder에서 점진적으로 복원
    - modified Xception Backbone: 각 채널마다 다른 필터를 사용하여 conv 연산 후 결합
  - U-net
    - 문제
      - 데이터 부족
        - 기존의 모델들은 많은 데이터가 필요
        - biomedical 특성상 데이터가 부족
      - 인접한 경계 구분이 어려움
      - U 형태의 Architecture
      - Data augmentation
        - Random Elastic deformations Augmentation(물체에 왜곡)
      - Pixel-wise loss를 계산하기 위해 Weight map 생성
      - 한계
        - 깊이가 4로 고정
        - 단순한 skip connection

---

# 피어세션
- 프로젝트 선정을 위한 회의
  - **자동차 번호판 deblurring**
    - ML 파이프라인 관점에서 더 디벨롭 해야함
    - Continuous 관점에서 사람에게 추천 영역을 제안하고 피드백 받기
  - **슬라이드쇼 to Audio**
    - 데이터셋 관련 문제 해결 필요
    - 영상마다 끊겨지는 구간에서 오디오가 끊어질지
    - 어떤 기술이 사용되어야하는지 조사 필요
      - CLIP?
    - 평가지표? -
      - 이런 부분은 오히려 ML파이프라인을 생각해봤을 때 직접 선정할 수 있어서 더 좋지 않을까?
      - 그래도 수치적으로 나올 수 있는
    - 서비스 관점의 시나리오 만들어보기
      - 왜 만들었는지도 중요
    - 유저 피드백
    - 이게 과연 CV 프로젝트인가??
  - **인물 영상 편집**
    - 영상 편집 시점으로 생각
      - 사람 별 tracking 후 관련 scene 선택
    - scene understanding 기술을 더 디벨롭 해보면 좋은 아이디어가 되지않을까?
      - 평가 지표가 애매해짐
      - Multi modal 없이는 힘들지 않을까??
        - LSTM을 사용했을 때 이미지만으로 가능할 것이라 예상됌
    - 얼굴 인식 부분은 어려울 것 같음
    - 서비스 관점 시나리오도 필요함
      - 학습 이후 베타 서비스를 해볼 예정이기 때문
  - **차량 불량 검수**
    - 시나리오가 부족함.
  - 생성 쪽 관련은 배제해야할 것 같음
  - ML Flow + Continuous learning + 경량화
    - 세 가지 조건이 맞춰진 환경에서 새로운 아이디어를 찾아보자
    - 주제: 적용할 수 있는 디바이스 관점 
      - CCTV, ~~ondevice~~, ~~모바일~~, 웹, ~~기타~~
    - Dacon, data 관점
- day2 (아이디어 브레인스토밍)
  - 레고 이미지 생성
    - text 2 image
    - iamge 2 3d image
  - 법정 제출용 영상 편집
    - 어린이집 CCTV 등
    - 기술요소 : detection, tracking, 
  - Ai Painter
  - youtube영상
    - 과거 축구영상 고화질 복원
    - 과거 애니메이션, 영화 컬러 등 고화질 복원
  - 배송용 로봇 자율주행
  - NeRF를 이용
    - RealMap Scanning (드론 자율주행 영상 사용)
    - lego render 3d modeling
  - person re-indentity
  - 야생동물 detection
  - 불안정한 도로 로드마크
    - 비온전 로드마크 -> 식별
    - 비온전 로드마크를 신고
  - 축구 경기 분석
    - 선수별 tracking
    - 농구 경기 심판?
- day3
  - 컴퍼니데이 후기 공유
    - 취업 걱정..
  - 보이저 엑스 기업 방문 겸 오프라인 모임 가지기!
  - P-stage
    - 이번 대회는 하고싶은 것들을 다 해보자라는 취지로 진행
      - 하고싶은 목록 정리


---
# 마스터 클래스 (김현우 마스터님)
- Segmentation 대회 소개 및 프리뷰
- 기존대회 분석
  - 한국인 헤어스타일
    - Co-teaching 기법
    - self cutmix
  - Body Morphometry2021
  - Hubmap
    - 상당히 큰 이미지
      - Sliding window
      - Detection 이후 segmentation 
      - Sampler -> mask가 있는 영역이 많이 추출되도록 sampler 구성
  - Cloud Understanding
    - Classification Head
      - encoder 부분에 Classification loss를 계산하여 사용
- 경진대회 분석
  - class imbalance 문제
    - Object Aug
  - 데이터에 노이즈가 많음
    - Data cleansing
  - boundary 및 클래스가 섞인 경우
    - DenseCRF
    - HRNet (High Resolution Network)
    - Multi Scale TTA
  - 앙상블 팁
    - 서로 상호 보완 관계를 가지는게 좋음
    - 다양성을 최대한 주는게 좋음


---

# 멘토링
- 국방 AI 수상 후 멘토링
  - 네이버 현직자 멘토링
  - 대회 내용 설명 및 피드백
  - 전반적인 현재 AI 서비스들 (네이버, KT, SKT 등등)
    - AI 스피커 + AI 돌봄 서비스 (SK, KT)
    - 클로바 케어콜 (AI 대회를 통해 대상자의 상태 확인 및 모니터링)
    - 현재 네이버랩스는 디지털 트윈 기술에 관심이 많음
  - 개발 기획 관점에서 B2B, B2C를 생각해보고 의미가 있는지
  - 전체적인 경기가 안좋아져서 취업시장이 어두운거지 AI는 어디에서나 사용됨
  - 좋은 회사를 가는건 물론 좋지만 회사를 차근히 step별로 옮기는 것도 좋음
- 지난 대회 리뷰 및 피드백
  - 간단 대회 내용 소개 / 다른 팀과 비교
    - 다른 팀보다 적은 데이터셋 임에도 좋은 성능이 나온 이유? 가설을 확실하게 알려면 운영진이나 마스터님에게 한번 문의해보기
- 이번 대회 내용
  - Point rend 처럼 가장자리를 잘 찾는 문제가 아닌 분류문제를 더 잘 잡는 것으로 연구 가중치를 둬야하지 않을까?
    - 백본? 모델? 어떤 class가 어려운지를 확인
- 최종 프로젝트 선정 피드백
  - 후보 주제 설명 후 피드백
    - CCTV 민감정보 블라인더
      - scene understanding 부분이 꽤나 어려워보임
      - 기획 배경은 크게 중요하지 않을지도 모름
    - 노면 표시 노후화 또는 크랙 인식
      - 1. 자율주행을 위한 노면 표시 인식
        - 비전으로 처리해야하는 문제인가? 지도에 표시되는것이 아닌가?
      - 2. 노후화 크랙 신고
        - 노면표시, 크랙에 대한 필요성은 있어보이지만 사용 시나리오에 대해 조금 더 구체화되야할듯
        - real time? 장단점이 있을듯
    - 배송로봇 자율주행
      - 아이디어를 작게 만들어보는 것이 어떤지 (차 -> 로봇청소기?)
      - 자율주행을 한다는게 창의성 면에서는 
- 논문 읽는 방법!
  - 스킵할건 스킵해야한다.
  - 논문 리스트를 만들기
    - 우선순위를 두고 순위가 떨어지는 논문은 skip
    - Yannic kilcher(유튜브), arxiv, github, 논문 목록 사이트
  - 1. 제목과 초록, 도표를 읽고 핵심을 파악
    - 우선순위 선정에 도움
  - 2. introduction, conculsion, figure 를 읽고 필요없는 부분은 과감하게 스킵
  - 3. 수식은 과감히 생략
    - 수학을 좋아하면 보는거도 나쁘지않음
  - 4. 이해가 안되는 부분은 빼고 전체적으로 읽어보기
  - 논문을 읽고 답변이 가능한지 확인
    - 저자가 뭘 해결하고자 하는가?
    - 이 연구의 핵심 접근방법이 무엇인지?
    - 논문의 아이디어를 어떻게 활용할 수 있는가?
    - 당신이 참고하고 싶은 다른 래퍼런스는 어떤 것인가?
  - 코드로 연습하기
    - 1. 오픈소스를 다운받아서 활용해본다.
    - 2. 밑바닥부터 직접 구현해본다.
  - 논문 스터디?
    - 다양한 의견을 들을 수 있다
    - 효율적이다. 필요하다면 돌려보기
    - 하지만 모두가 완벽하게 해올까..?
  - 멘토님의 방법
    - 순차적으로 읽어가면서 중간마다 다음 방향을 예상해봄(나였다면 어떤식으로 해결할까?)
  - 관심분야의 Survey 논문
    - Survey에는 얇고 넓은 관점이 있음

---

# 스페셜 피어세션 (Boost up)
- 팀별 아이디어를 공유해보자
  - 항상 대회가 끝이나고 공유가 되는게 아쉬워서
- 이외의 자유주제 : 번아웃, 최종 프로젝트 주제 선정?

---
### 참고자료
- 부스트캠프 AI Tech 교육 자료