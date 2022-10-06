---
title: Boostcamp 13days
date: 2022-10-06 18:00:00 +0900
comment: true
categories: [Boostcamp AI Tech 4기]
tags: [3weeks, 13day]
math: true

---
# 13일차 학습 정리

<h3 data-toc-skip> 시각화, 기본적인 차트 </h3>

- Matplotlib을 통해 간단한 시각화 실습 (1-3)
- **Bar Plot 사용하기**
  - 막대그래프
    - 범주에 따른 수치 값을 비교하기에 적합
      - 개별비교, 그룹비교 등
  - 수직[.bar()]과 수평[.barh()]
  - 여러개의 그룹을 보여줄 땐 여러가지 방법이 있음
    - Stacked Bar Plot
      - 그룹을 쌓아서 표현하는 bar plot
      - bottom, left파라미터 사용
      - 전체적인 모습은 포기 편하지만 아래 분포 이외의 분포들이 파악이 어려움
        - Percentage Stacked Bar Chart
          - 전체에 비율을 나타내는 차트
    - Overlapped Bar Plot
      - 2개 그룹만 비교할때, 겹쳐서 표현
    - Grouped Bar Plot
      - 그룹별 범주에 따른 Bar를 이웃되게 배치하는 방법
      - [ .set_xticks(), .set_xticklabels() ]
      - 그룹이 5~7개 이하일 때 효과적
  - Bar Plot의 원칙
    - 실제 값과 그에 표현되는 그래픽으로 표현되는 잉크 양은 비례해야 함
      - 반드시 x 축의 시작은 0(zero)!
    - 데이터 정렬하기
      - pandas에서는 sort_values(), sort_index()를 사용하여 정렬
    - 적절한 공간 활용
      - 여백과 공간만 조정해도 가독성이 높아진다.
      - Matplotlib techniques
        - X/Y axis Limit (.set_xlim(), .set_ylime())
        - Spines (.spines[spine].set_visible())
        - Gap (width)
        - Legend (.legend())
        - Margins (.margins())
    - 복잡함과 단순함
      - 무의미한 복잡함은 필요없음
      - 시각화를 보는 대상이 누구인가?
        - 정확한 차이 (EDA)
        - 큰 틀에서 비교 및 추세 파악 (Dashboard)
      - 축과 디테일 등의 복잡합 (축, 레이블, 텍스트)
  - bar plot 실습
- **Line Plot 사용하기**
  - 꺾은선 그래프, 선그래프
    - 연속적으로 변화하는 값을 순서대로 점으로 나타내고 이를 선으로 연결한 그래프
    - 시계열 분석에 특화
    - .plot()
  - 요소
    - 색상(color), 마커(marker, markersize), 선의 종류(linestyle, linewidth)
  - 노이즈
    - 시시가각 변동하는 데이터는 노이즈가 많아 패턴 및 추세 파악이 어려움
    - Smoothing 사용
  - 추세에 집중
  - 간격
    - 규칙적인 간격 - 만약 아니라면 점으로 표시하여 오해 줄이기
  - 보간
    - 점과 점 사이의 데이터를 잇는 방법
    - error 나 noise가 포함되어 있는 경우, 데이터의 이해를 도움
  - 이중 축 사용
  - line plot 실습
- **Scatter Plot 사용하기**
  - 산점도
    - 점을 사용하여 두 feature간의 관계를 알기 위해 사용하는 그래프
    - .scatter()
  - 요소
    - 점(color), 모양(marker), 크기(size)
  - 목적
    - 상관 관계 확인
    - 군집(cluster), 값 사이의 차이(gap in values), 이상치(outliers) 확인
  - Overplotting
    - 점이 많아질 수록 점의 분포를 파악하기 힘듦
      - 투명도 조정, 지터링(jittering), 2차원 히스토그램(히트맵 형식), Contour plot(등고선 그래프)
  - 점의 요소와 인지
  - 인과관계와 상관관계
    - 두 관계는 다름
  - 추세선
  - scatter plot 실습

---

# 심화 과제
- VIT (Vision Transformer)
  - Vision Transformer 구현 실습
  - Multi-headed Attention 구현
  - Attention map 확인
  


---
# 마스터 클래스

- 교수님이 살아온 경험
  - 가난한 대학원생이 교수가 되기까지 (강사 경험)
  - 근 미래의 내가 조금 힘들어질 수 도 있는 결정을 해보자!
- AI 엔지니어가 되고 싶다면 해당 분야의 SOTA 장단점을 정확히 파악하고 이를 활용해 응용할 수 있어야한다!
- 최근 트랜드, 동향
  - 요즘은 transformer 가 굉장히 많이 사용된다
  - 결국 데이터가 중요! data centric ai
  - 변화에 민감한 것 보다 문제를 정확히 정의하고 이어나가는 것이 중요하다고 생각 (어차피 변화는 빠르기 때문)

# 피어세션
- 수업 관련
  - 심화 과제에 대한 궁금증 공유
  - 팀원 토의 중 해결 되지 않는 문제들은 오피스아워 시간에 질문 예정
- 팀 대회
  - 구글 드라이브 속도 문제
- [회의록](https://night-eustoma-5f3.notion.site/10-06-7432cbe517bf40f88095ad9702041caf)


---

### 참고자료
- 부스트캠프 AI Tech 교육 자료