# Lending Club

## Data

**lending_club_2020_train.csv**
: 미국의 P2P 대부업체인 Lending Club에서 공개된 2007-2020의 자료의 60%, 나머지 40%는 test data 용도로 최종 발표일 1주일 전에 다시 공지.

**Lending_club_variables.txt**
: 변수 설명이 담긴 자료.

1. test data로 평가하는 것인가?
2. Sharpe ratio를 극대화 하는 것 vs 부도 여부를 예측하는 것 vs Sharp ratio를 이용해서 부도 여부를 예측하는 것?

## Objective

특정 개인이 부도 상태인지 아닌지 구분하는 모형을 수업에서 배운 통계적 기법들을 총 동원하여 구축.

Lending Club에서 부도예측을 했다면 투자 결정 당시의 3년/5년 만기 미 국채에 투자하였다고 가정 (다른거 해도 됨) merge하려면 시간이 중요함.

상환구조는 원리금균등상환

cash flow를 현재 투자 시점으로 할인하여 모두 더하여 새로이 계산한 이자율(수익률) r을 내부수익률이라고 함. 이걸 이용하는 것을 기본 골자로 하시길 바란다. 여기서 초과수익률을 구할 수 있다.

목적함수: Sharpe ratio를 극대화

1. 데이터 전처리
2. train-set을 이용해 '여러'모형을 구축한다.
3. validation set으로 최적의 모형을 위해 hyperparameter 등을 튜닝
4. test set으로 검증

## Variables

| variables            | description          |
| -------------------- | -------------------- |
| term                 | 대출 실행 기간             |
| grade                | 신용등급                 |
| annual_inc           | 연간소득                 |
| home_ownership       | 거주 자가 형태             |
| purpose              | 대출의 목적               |
| emp_length           | 근로 연수                |
| dti                  | 소득 대비 부채 비율          |
| pub_rec              | 공공 기록 수 (신용에 부정적인 것) |
| pub_rec_bankruptcies | 파산 관련된 공공 기록 수       |
| open_acc             | 현재 거래 중인 계좌의 수       |
| mort_acc             | 모기지 실행 중인 계좌의 수      |
| revol_util           | 리볼빙 사용률              |
| revol_bal            | 리볼빙 잔액               |
| fico_range_low       | FICO 신용점수의 하한        |
| inq_last             | 최근 6개월간 신용조회 횟수      |
| verification_status  | 신청자 소득 정보 확인 단계      |
| exess_return         | 초과수익률                |


## Sharpe ratio


Sharpe ratio: 위험(=변동성) 대비 초과수익율

$$ S = \frac{E[R-R_{f}]}{\sqrt{\operatorname{Var}[R-R_{f}]}} = \frac{R_{p}-R_{f}}{\sigma_{p}}$$

| symbol           | desc                                             |
| ---------------- | ------------------------------------------------ |
| ${ R}$           | asset return                                     |
| ${ R_{f} }$      | risk-free return                                 |
| ${ R-R_{f} }$    | asset excess return                              |
| ${ E[R-R_{f}] }$ | expected asset excess return                     |
| ${ \sigma_{p} }$ | risk = standard deviation of asset excess return |
## Models

[Principal component analysis - Wikipedia](https://en.wikipedia.org/wiki/Principal_component_analysis): 이걸로 주요한 변수만 뽑아보자 (overfitting 해결?)

[Reinforcement learning - Wikipedia](https://en.wikipedia.org/wiki/Reinforcement_learning)

[Kernel method - Wikipedia](https://en.wikipedia.org/wiki/Kernel_method)

[Nonlinear dimensionality reduction a.k.a manifold learning - Wikipedia](https://en.wikipedia.org/wiki/Nonlinear_dimensionality_reduction)

[Neural network (machine learning) - Wikipedia](https://en.wikipedia.org/wiki/Neural_network_\(machine_learning\))

[k-means clustering - Wikipedia](https://en.wikipedia.org/wiki/K-means_clustering)

데이터 전처리

모델 구상

데이터 전처리 다음주 월요일

