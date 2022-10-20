---
title: Boostcamp 20~21days
date: 2022-10-19 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [5weeks, 20day, 21day]
math: true

---

# Github 특강 2
- 이고잉(egoing)님의 특강 (생활코딩)
- 깃을 활용한 협업 관리

---

# 20, 21일차 학습 정리

<h3 data-toc-skip> Multi-modal </h3>

- 서로다른 도메인을 활용하여 학습하는 것
- 어려운점
  - 데이터의 표현 방법이 다 다름
  - feature spaces가 다름
  - 모델이 한 도메인에 편향을 가지기 쉬움
- Text (Multi-modal)
  - Text embedding
    - 단어를 학습하기 위해 벡터화
    - 일반화를 할 수 있다.
    - word2vec
      - Skip-gram model
      - 주변 N개의 word의 관계성을 학습
      - Embedding vector 추출
  - Joint embedding
    - Image tagging
      - 이미지를 활용하여 태그를 생성하거나 그 반대
      - 서로 다른 도메인으로 학습된 모델 사용
      - 각 모델에서 추출된 피쳐를 Joint embedding 영역에 맵핑
      - 서로의 피쳐를 매칭하여 관계를 학습
    - Image & food recipe
      - 문장의 대표하는 피쳐와 이미지를 대표하는 피쳐를 추출
      - Cosine similarity loss
        - 두 피쳐의 유사성을 학습
      - semantic regularization loss
        - high-level semantics
        - cosine loss로 학습되지 않는 부분을 도움
  - Cross modal translation
    - Image captioning
      - 이미지를 설명하는 문장으로 변환
      - Show and tell
        - Encoder => CNN
        - Decoder => LSTM
      - Show, attend, and tell
        - Attention을 추가
          - CNN 피쳐를 RNN에 넣어 Soft Attention map 추출
          - CNN의 피쳐에 Soft Attention map에 맞게 가중치
    - Text to image
      - generative model이 필요함
      - 문장을 주고 이미지를 여러개 추출
  - Cross modal reasoning(Referencing)
    - Visual question answering - Multiple streams
      - image stream과 text stream 이용
- Audio (Multi-modal)
  - Sound representation
    - Fourier transform 사용
      - Short-time Fourier transform (STFT)
      - 주파수 성분을 분석하기 쉽게 해줌
    - Spectrogram
      - 시간에 따라 스팩트럼을 쌓음
      - 시간에 따른 주파수 성분을 눈으로 분석하기 쉽게함
  - Joint embedding
    - Scene recognition by sound
      - 사운드를 통해 장면을 추측
      - Sound Net
        - 물체와 장소 두개의 헤드 사용
        - Teacher(CNN) - student(sound) 학습법
        - pool5 feature를 사용하여 다른 task로 활용 가능
  - Cross modal translation
    - Speech2Face
      - 연설을 듣고 얼굴을 추측
      - Module entworks
      - Voice Encoder 가 Face Encoder를 따라하도록 학습
      - Voice Encoder -> Face Decoder
    - Image to speech
      - Show, Attend and Tell 모델 활용
      - Tacotron 2 (TT2)로 Unit to Speech 모델 활용
      - 두 모델간의 사이 유닛의 호환성을 적절히 학습
  - Cross modal reasoning
    - Sound source localization
      - 이미지에 사운드가 어디서 들리는지 추측
      - Visual net과 Autio net 사용
      - 두 피쳐를 Attention net을 통해 관계성을 학습
      - supervised, unsupervised, semi-supervised 등 여러 학습 방법이 존재
- 자율 주행(여러 센서 + video) 처럼 multi-modal 모델은 다양하게 응용할 수 있다.
- Image captioning 구현 실습
  - Encoder
    - CNN + RNN
  - Decoder
    - attention 정보와 입력토큰(이전 단어)를 입력으로
  - Beam search
    - decode step마다 스코어 top k 문장을 선택

---

# 기본과제
- cGAN (기본-4)
  - Conditional GAN을 활용하여 Mnist 생성
  - cGAN 논문을 베이스로 코드 실습
  - 각자 구현 방식에 따라 성능이 달라짐
    - 성능 향상을 위해 시간이 소요..
- Pre trained Multi modal Model Applications with CLIP
  - CLIP을 활용한 Multi-modal model 실습
  - Image Classification
  - Image-Text Matching Task
  - Text2Image 모델 학습 및 활용

---

# 멘토링
- ML에 도움을 주는 라이브러리 리뷰
  - einops
    - einops 사용 방법과 그 예시들 확인
  - Automatic Mixed Precision(AMP)
    - Mixed precision 동작 방식
    - 동작 순서 및 사용 예시
    - 성능 비교
- 팀 빌딩 과정 공유
  - 각자 생각하는 주제를 공유


---

# 피어세션
- 팀 빌딩 진행사항 공유
  - 아이디어 주제 토론
- 수업 관련
  - 과제 4 성능 관련 질문
  - 과제 5 clip모델에 관한 토론
- [20day 회의록](https://night-eustoma-5f3.notion.site/10-18-b1956042291f4cf1a0a3907e3585f72a)
- [21day 회의록](https://night-eustoma-5f3.notion.site/10-19-8f54c6b7c920481e90be2a0405fccbf3)

---

### 참고자료
- 부스트캠프 AI Tech 교육 자료