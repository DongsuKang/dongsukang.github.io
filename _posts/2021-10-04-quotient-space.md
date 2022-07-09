---
title:  "몫 공간(Quotient space)"
excerpt: "선형대수학의 몫 공간에 대해 정리해보자"

categories:
  - Linear Algebra

toc: true
toc_sticky: true

use_math : true
comments : true
image : true
sitemap :
changefreq : daily
date: 2021-10-04
last_modified_at: 2021-10-08
---


## 들어가기 전에
최근 선형대수학 세미나에서 발표하며 복습 하게 된 개념, quotient space에 대해 이번 기회를 빌려 정리해보고자 한다.

## coset이란?
몫 공간에 대한 설명 이전에 앞서 coset에 대한 정리가 필요하다. 몫 공간의 벡터의 형태는 모두 이 coset의 형태를 하고 있기 때문이다. coset은 국내 교재에서는 '잉여류'라고 하는데, 잉여류라고 할 때보다는, coset이라고 할 때 그 의미가 더 와 닿는 것 같아서, coset라고 적도록 하겠다.

어떤 벡터공간 V가 있고, 이 V의 부분공간을 W라고 하자. 벡터 공간 V에서 임의의 벡터 $\mathbf{v}$ 가 있을 때, $\mathbf{v} + W := \\{ \mathbf{v} + \mathbf{w} \ |  \ \mathbf{w} \in W \\}$ 인 벡터 집합을 coset 이라고 한다.
그리고 이 때, V에서 임의 선택한 벡터 $\mathbf{v}$ 를 coset을 대표한다고 해서 representative라고 한다. (아마 coset이라는 set이 임의 선택한 벡터에 종속되어 있기 때문이 아닐까 한다.)

정의를 보면 알겠지만, coset은 V에서 어떤 벡터를 가지고 오느냐에 따라 그 값이 바뀌는, 즉, $\mathbf{v}$에 종속적일 수 밖에 없는 정의를 가지고 있다.

앞서 오늘의 주요 토픽인 몫 공간의 벡터가 coset의 형태를 하고 있기 때문에, 몫 공간 설명 이전에 앞서 coset을 설명해야 한다고 했다.

그리고, coset과 관련된 2가지 증명을 소개하고자 한다.

1. $\mathbf{v} + W$가 V의 부분공간이 되기 위한 필요 충분 조건은 $\mathbf{v} \in W$ 와 같다.
  - $\mathbf{v} + W$가 V의 부분공간이 되는지 보이기 위해서 '연산에 대해 닫혀있음'을 의미하는 subspace test를 해보면 이 증명이 성립하는지 알 수 있다.

2. $\mathbf{v}_1 + W = \mathbf{v}_2 + W$ 이기 위한 필요충분조건은 $\mathbf{v}_1 - \mathbf{v}_2 \in W $ 이다.
  - $\mathbf{v}_1, \mathbf{v}_2 \in V$ 이고, $\mathbf{v}_1 + W = \mathbf{v}_w + W $ 라고 가정해보자. 이 명제의 필요 충분 조건은 $(\mathbf{v}_1 - \mathbf{v}_w) + W = W$ 임을 알 수 있다. 왜냐하면, 양 옆에 $-\mathbf{v}_1$을 더해서 $-\mathbf{v}_1 + \mathbf{v}_2 + W = W$를 만들어 주면, 등호를 만족 시켜주기 위해서는 $-\mathbf{v}_1 + \mathbf{v}_2 \in W$ 여야 하기 때문이다. 따라서 두 개의 representative끼리의 차이가 W에 있어야 하고,  $\mathbf{v}_1 + \mathbf{v}_2 \in W$ 라고 가정하면, $(\mathbf{v}_1 - \mathbf{v}_w) + W = W$ 을 만족함을 보이면서 명제의 역 또한 증명할 수 있다.

### coset의 덧셈, 스칼라곱 정의
coset의 덧셈과 스칼라곱은 아래와 같이 정의한다.

- 모든 $\mathbf{v}_1, \mathbf{v}_2 \in V$ 에 대하여 $ ( \mathbf{v}_1  + W) + ( \mathbf{v}_2  + W) = (\mathbf{v}_1 + \mathbf{v}_2) + W$

- 모든 $\mathbf{v} \in V$ 와 $a \in F$ 에 대하여 $a(\mathbf{v} + W) = a\mathbf{v} + W$

즉, coset의 덧셈과 곱셈은 coset의 representative끼리의 덧셈과 스칼라 곱처럼 취급하겠다는 의미이다.

## 몫 공간(quotient space)이란?
coset의 덧셈, 스칼라곱 정의를 기반으로 coset을 벡터로 하는 벡터공간을 몫 공간(quotient space)이라고 한다.
사실 coset을 공부하는 순간, 몫 공간의 정의에 대해서는 크게 할 것은 없다.

## 그래서 몫 공간이 뭐지?

몫 공간에 대한 이해도를 높이기 위해서는 몫 공간의 기저와, null space에 대해 알 필요가 있다.

### 몫 공간의 기저

벡터 공간 V의 부분 공간 W의 기저를 $\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_k$ 라고 하자.(W의 dimension은 k이다.). 그리고 basis extention thorem을 통해 W의 기저를 확장하여, V의 기저를 만든다. 그 형태는 다음과 같다.

$$\\{ \mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_k, \mathbf{v}_{k+1}, \mathbf{v}_{k+2}, \ldots, \mathbf{v}_{n} \\}$$

당연히 V의 dimension은 n이다.

이 때 V/W의 기저는 다음과 같다.

$$\\{ \mathbf{v}_{k+1} + W, \mathbf{v}_{k+2} + W, \ldots, \mathbf{v}_{n} + W\\}$$

### 몫 공간의 null space

벡터 공간 V와 부분 공간 W에 대해서 함수 $\eta : V \rightarrow V/W$를 다음과 같이 정의한다.

$$\mathbf{v} \in V, \eta(\mathbf{v}) = \mathbf{v} + W$$

이 때, 함수 $\eta$는 전사인 선형변환이고, 동시에 $N(\eta) = W$는 이다. 선형 변환인 $\eta$에 dimension theorem을 적용하면, 다음과 같은 관계식을 얻을 수 있다.

$$ dim(V/W) = dim(V) - dim(W) $$

정리하면, 어떤 벡터공간 v의 부분공간 w를 이용해 v/w 형태의 몫 공간을 만든다면, 이 몫 공간의 dimension은 dim(V) - dim(W) 이다. 그리고, dimension이 basis의 개수이고, basis가 벡터 공간의 모든 벡터를 선형 결합으로써 표현 가능하다는 사실을 연결해보면... V/W는 벡터 공간 V와 W의 공간에서 경계선이 지어져 있는 형태임을 알 수 있다. 즉, partitioning 되어 있다는 뜻이다. (계속)





>Reference
>\- 스티븐 H.프리드버그, 아놀드 J.인셀, 로렌스 E, 스펜스, 『프리드버그 선형대수학 5판』,한빛 아카데미(2020)
