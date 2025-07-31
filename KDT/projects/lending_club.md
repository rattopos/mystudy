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

## 회귀

weight 

손실함수 어떻게 할 것인지 생각하기

raw 데이터로 번호 1 ~ 25 변수의 특성을 찾아오자 (이상한 것, 특징)

원핫인코딩 -> 뉴욕 LA clolum 하나씩 

이것때문에 변수가 늘어남

월상환을 연이율로 바꿔서 risk-free와 비교

예측되는 확률값의 cut-off의 sharpe ratio가 대략적으로 얼마가 얻어지는가?

## 2025-07-30

1~25 데이터

```python
Dict = pd.read_excel('d.xlsx')

data = pd.read_csv('lending_club_2020_train.csv')


col = list(Dict['LoanStatNew'][:10])
col.append('loan_status')
data = data[col]


df = data[data['loan_status'].isin(['Fully Paid', 'Charged Off', 'Default'])]
status_map = {
    'Fully Paid': 0,
    'Charged Off': 1,
    'Default' : 1
}



df['loan_status'] = df['loan_status'].map(status_map)

import matplotlib.pyplot as plt
import numpy as np
cols = df.columns
n_cols = 2  # 한 행에 2개
n_rows = (len(cols) + n_cols - 1) // n_cols  # ceil 나눗셈

fig, axes = plt.subplots(n_rows, n_cols, figsize=(n_cols*5, n_rows*4))
axes = axes.flatten()  # 2D 배열을 1D로 펼침

target_col = 'loan_status'

df = df.fillna(-1)
for i, col in enumerate(cols):
ax = axes[i]

# 범주형 또는 고유값이 적은 컬럼
if df[col].dtype == 'object' or df[col].nunique() < 30:
    # 범주형: loan_status=1 비율 계산 (상위 30개만)
    # 문자열 '-1' 값도 일반 범주처럼 처리
    df[col] = df[col].fillna('Unknown') # NaN을 'Unknown'으로 처리

    top_cats = df[col].value_counts().index[:30]
    filtered = df[df[col].isin(top_cats)]
    # 그룹화 시 NaN 처리된 '-1'도 하나의 범주로 포함될 수 있음
    grouped = filtered.groupby(col)[target_col].mean()
    grouped.plot(kind='barh', ax=ax, color='skyblue', edgecolor='black')
    ax.set_xlabel('P(loan_status=1)', fontsize=9)
    ax.set_ylabel('')
    ax.set_title(f'Categorical: {col}', fontsize=10)
    ax.tick_params(axis='y', labelsize=8)
    ax.tick_params(axis='x', labelsize=8)

else:
    # 연속형 컬럼 - -1 값 분리 및 분위수 binning
    df_no_neg1 = df[df[col] != -1].copy() # -1이 아닌 값들만 복사하여 사용
    df_neg1 = df[df[col] == -1].copy() # -1인 값들만 복사

    # -1 값에 대한 loan_status=1 비율 계산
    neg1_ratio = None
    if not df_neg1.empty:
        neg1_ratio = df_neg1[target_col].mean()

    # -1이 아닌 값들에 대한 분위수 binning
    if not df_no_neg1.empty:
        # duplicates='drop'을 사용하여 동일한 경계값이 있을 경우 드롭
        bins = pd.qcut(df_no_neg1[col], q=10, duplicates='drop', precision=0) # 10분위로 변경 (좀 더 세밀하게)
        grouped_bins = df_no_neg1.groupby(bins)[target_col].mean()

        # x축 라벨을 위한 인덱스 생성 (보기 좋게)
        bin_labels = [f'{b.left:.0f}~{b.right:.0f}' for b in grouped_bins.index]
    else:
        grouped_bins = pd.Series(dtype=float)
        bin_labels = []

    # -1 값 결과를 통합
    final_grouped_data = {}
    if neg1_ratio is not None:
        final_grouped_data['-1'] = neg1_ratio
        final_labels = ['-1'] + bin_labels
    else:
        final_labels = bin_labels

    # 분위수 데이터 추가
    for i, (label, value) in enumerate(zip(bin_labels, grouped_bins.values)):
        final_grouped_data[label] = value

    # 순서를 지키기 위해 OrderedDict 또는 직접 순서 지정
    # 딕셔너리를 사용하여 순서를 유지하고 Series로 변환
    plot_data = pd.Series(final_grouped_data)

    # '-1'이 있다면 가장 앞으로 이동
    if '-1' in plot_data.index:
        plot_data = plot_data[['-1'] + [idx for idx in plot_data.index if idx != '-1']]

    plot_data.plot(kind='line', marker='o', ax=ax, color='orange')
    ax.set_ylabel('P(loan_status=1)', fontsize=9)
    ax.set_title(f'Continuous: {col}', fontsize=10)

    # x축 레이블 설정
    ax.set_xticks(range(len(plot_data)))
    ax.set_xticklabels(plot_data.index, rotation=45, ha='right', fontsize=8) # 레이블 회전 및 정렬
    ax.set_xlabel(col, fontsize=9)

```

결측치, 다중공분산, 