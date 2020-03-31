# House Pricing 

## Comprehensive data exploration with Python 공부

링크 : https://www.kaggle.com/pmarcelino/comprehensive-data-exploration-with-python

### 논리 이해하기
1. 문제 이해 : 최종적인 집 값 예측하기

2. 전처리

(1) 분석하기

Variable (변수)

Data Type : numerical, categorial 

Segment : building (OverallQual), space(TotalBsmtSF), location(Neighborhood)

Expectation : 'SalePrice' 확률 (High, Medium, Low)

(2) 독립변수 뽑아내기

3가지 질문 (집을 살 때 생각하는 변수, 그 변수의 중요성, 중복되는지)을 통해 선정

OverallQual(Building), YearBuilt(Building), TotalBsmtSF(Space), GrLivArea(Space).

*Location변수를 고르지 않은 이유 : 카테고리형 데이터이기 때문

3. 종속변수(Sale Price) 분석하기

(1) 평균과 떨어져 있음

(2) 특징적인 편포도를 가짐

(3) 편포도 : 1.88 / 첨도 : 6.53

(4) 독립변수와의 관계 

모두 상관관계 높음

Numerical : GrLivArea < TotalBsmtSF

Categorial : OverallQual > YearBuilt

(5) 다른 변수들간의 상관관계 



4. 데이터 정리하기

5. 가설 검증하기

### 코드의 흐름

#### 불러오기

import pandas as pd

import matplotlib.pyplot as plt

#통계적 데이터 비쥬얼라이제이션 : https://seaborn.pydata.org/

import seaborn as sns 

import numpy as np

#통계적 데이터 비쥬얼라이제이션 : https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.norm.html

http://localhost:8888/notebooks/Data%20Study/House%20Pricing/spicy.stats.norm.ipynb

from scipy.stats import norm 

#스케일링 : https://mkjjo.github.io/python/2019/01/10/scaler.html

from sklearn.preprocessing import StandardScaler

#가장 보편적인 값 찾기 : https://m.blog.naver.com/PostView.nhn?blogId=magnking&logNo=221282668005&proxyReferer=https%3A%2F%2Fwww.google.com%2F

from scipy import stats

#경고 메시지 숨기기

import warnings

warnings.filterwarnings('ignore')

#notebook을 실행한 브라우저에서 바로 그림을 볼 수 있게 해주는 것 : https://korbillgates.tistory.com/85

%matplotlib inline

#### Sale Price 분석하기

df_train['SalePrice'].describe()

sns.distplot(df_train['SalePrice']);

print("Skewness : %f" %df_train['SalePrice'].skew())

print("Kurtosis : %f" %df_train['SalePrice'].kurt())

#### GrLivArea와 SalePrice 분석하기

var = 'GrLivArea'

data = pd.concat([df_train['SalePrice'],df_train[var]],axis=1)

data.plot.scatter(x=var,y='SalePrice',ylim=(0,800000))

#### TotalBsmtSF 도 SalePrice 와 함께 분석하기

var = 'TotalBsmtSF'

data = pd.concat([df_train['SalePrice'],df_train[var]],axis=1)

data.plot.scatter(x=var,y='SalePrice',ylim=(0,800000))

#### OverallQual 과 SalePrice 분석하기

var = 'OverallQual'

data = pd.concat([df_train['SalePrice'],df_train[var]],axis = 1)

f, ax = plt.subplots(figsize = (8,6))

fig = sns.boxplot(x=var,y="SalePrice",data=data)

fig.axis(ymin=0,ymax=800000)

#### YearBuilt 와 SalePrice 분석하기

var = 'YearBuilt'

data = pd.concat([df_train['SalePrice'], df_train[var]], axis=1)

f, ax = plt.subplots(figsize=(16, 8))

fig = sns.boxplot(x=var, y="SalePrice", data=data)

fig.axis(ymin=0, ymax=800000);

plt.xticks(rotation=90);

#### 변수 간의 상관관계 분석하기

혹시 다른 변수가 있나 보려는 의도!!




### 지식 보충

