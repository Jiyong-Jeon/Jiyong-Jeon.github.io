---
title: Boostcamp 34days
date: 2022-11-08 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [8weeks, 34day]
math: true

---

# 34일차 학습 정리

<h3 data-toc-skip> Voila </h3>

- 프로토타입
  - 모델을 개발한 후, 사람들과 테스트할 수 있는 프로토타입을 먼저 만듬
  - Notebook 베이스로 프로토타입 만들기
    - Voila
    - 단기간내에 Notebook 환경 그대로 프로토타입이 만들어짐
- 장점
  - Notebook에서 별도의 코드 추가 없이 실행할 수 있음
  - Ipywidget, Ipyleaflet 등 사용 가능
  - Jupyer Notebook의 Extension 있음 (= 노트북에서 바로 대시보드로 변환 가능)
  - Python, juila, c++ 코드 지원
  - 고유한 템플릿 생성 가능
  - 너무 쉬운 러닝커브
- Voila 사용 팁
  - 강의 자료 참고하여 복습해보기
- Ipywidget
  - 인터렉티브한 효과
  - Widget 종류
    - Slider Widget, Text Widget, Boolean Widget, Selection Widget, Upload Widget, Image Widget, Date Picker Widget
  - Widget Events
    - on_click, observe, 
  - Interact Decorator
  - Layout
    - HBox, VBox
- Voila 실습
  - [실습 코드 Git](https://github.com/zzsza/Boostcamp-AI-Tech-Product-Serving)

<h3 data-toc-skip> Streamlit </h3>

- 빠르게 웹 서비스를 만들 수 있음
- 장점
  - 파이썬 스크립트 코드를 조금만 수정하면 웹을 띄울 수 있음
  - 백앤드 개발이나 HTTP 요청을 구현하지 않아도 됨
  - 다양한 Componet 제공
  - Streamlit Cloud 존재 (쉽게 배포)
  - 화면 녹화 기능(Record) 존재
- 컴포넌트 예시
  - https://docs.streamlit.io/
- Session State
  - 인터렉션이 있다면 코드가 재실행
  - Session State에 변수가 있다면 재실행 하여도 저장됨
- Streamlit Cache
  - @st.cache
  - 캐싱을 해줌
- Streamlit 실습
  - 실습코드는 위에 주소

<h3 data-toc-skip> Linux & Shell Command </h3>

- Linux
  - 배포판
    - Devian, Ubuntu, Redhat, CentOS
- Shell command
  - 쉘 종류
    - sh, bash, zsh
  - 기본 쉘 커맨드 (자주 사용)
    - man, mkdir, ls, pwd, cd, echo, vi, bash, sudo, cp, mv, cat, history, find, export, alias
  - 쉘 커맨드
    - head, tail, sort, uniq, grep, cut
  - 표준 스트림(Stream)
  - Redirection (>, >>) & Pipe ( | )
  - 서버에서 자주 사용하는 쉘 커맨드
    - ps, curl, df -h, scp, nohup, chmod
  - 쉘 스크립트

---

# level2
- 국방 AI 대회 진행
  - 데이터셋 공개
    - 라벨, 라벨 위치 등 데이터셋 특성을 파악하는 EDA 진행
    - EDA 결과와 기존에 준비한 모델에 맞게 데이터 전처리 

---

# 피어세션
- 강의 내용 공유
  - 실습 5번, 6번 오류
    - 주로 버전 문제 
    - 해결 방안 공유
- [회의록](https://night-eustoma-5f3.notion.site/11-8-609e543fe7fc4720ad47080a318dfc63)

---

# 부캠에서 살아남기
- 부캠 수료생이 알려주는 부캠에서 더 밀도있게 성장하는 법
- 전경민(CV) : 인공지능 어린이에서 인공지능 청소년되기
  - 프로젝트 협업 방식
    - Notion + Github + Slack + WandB
    - 특정 파트부터 시작하기
    - 깃 컨벤션 중요
  - 부캠을 통한 성장, 얻어가야할 것
    - 경험, 자신감, 미래 설계, 인맥
  - Task 변화 과정 흐름 관찰해보기, 분야 확장
- 김소연(NLP) : 부스트캠프 101
  - AI를 밀도있게 배우기 위해 질문왕되기
  - 부캠 생활, 프로젝트 진행 경험 소개
  - 하는 일이 많은거같다? 가치없어 보인다? 그런거 없이 다 소중하다.
  - 프로젝트 어필방법
    - 청자(기획자? 엔지니어?)가 누구인지, 프로젝트의 강점이 무엇인지에 중점
  - 나를 어필하는 방법
- 임경태(ResSys) : 지속가능한 성장 동력을 가진 개발자 되기
  - 후회없이 최선을 다하자
  - 항상 목표를 생각하고 움직이자
    - 작은 목표라도 설정하며 한 걸음씩 나아가자
  - Daily Check List 작성해보기
  - 꾸준함
    - 부캠의 모든 파트를 집중해야함
    - 부캠은 취업 보장을 해주지 않음
      - 코테, 면접 준비도 당연히 필수
  - 기록
    - 일어나는 모든 일들을 기록하기
    - Wrap-up report도 아주 중요
      - 잘 짜여진 스토리가 필요 (목표->수행 내용->결과->회고 및 Future Work)
      - 논리에 결함이 없어야함
  - 동료
    - 협업, 학습, 공유 모든 부분에서 동료는 항상 중요
    - 면접 대비의 수단으로도 사용가능
      - 기술 설명, 본인 소개 (스페셜 피어세션, PR연습!)
  - 부캠을 단순 취업 목표로 생각하지 말기
  - 과정에 집중하고 FOMO(fearing of missing out)에 빠지지 않기
  - 주변 인적 자원 100% 활용하기!
      


---
### 참고자료
- 부스트캠프 AI Tech 교육 자료