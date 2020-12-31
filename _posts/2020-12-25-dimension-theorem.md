---
title:  "차원정리(dimension theorem)"
excerpt: "선형대수의 차원 정리에 대해 공부해보자."

categories:
  - Linear Algebra

toc: true
toc_sticky: true

use_math : true
comments : true

sitemap :
changefreq : weekly

date: 2020-12-25
last_modified_at: 2020-12-25
---

## 들어가기 전에

차원 정리는 일종의 nullity와 rank의 관계를 표현하는 정리라고 할 수 있다. 여기서 nullity 와 rank의 정의는 각각 N(T)와 R(T)의 차원이고, kernel과 image의 정의는 아래와 같다.

> **정의** 벡터공간 V,W와 선형 변환 T : V $\to$ W 에 대하여
> - 영공간(null space 또는 kernel) 은 $T(x) = 0$인 $x \in V$를 원소로 가지는 집합이고 N(T)라 표기하나. 집합으로 나타내면 N(T) = {$x \in V \ \| \ T(x) = 0$}
> - 상공간(range 또는 image)은 T의 함숫값을 원소로 가지는 W의 부분집합이고, R(T)라 표기한다. 집합으로 나타내면 R(T) = {$T(x) \ \| \ x \in V$}


## 차원 정리(Dimension Theorem)란?

실제 차원 정리의 내용은 아래와 같다.

>**Thm** 벡터공간 V, W와 선형변환 T : V $\to$ W에 대하여, V가 유한차원이면 다음이 성립한다.
> <center>$$nullity(T) + rank(T) = dim(V)$$</center>

위에서 언급한 바와 같이, 정의역 V의 차원을 기준으로 nullity는 dim(V) - rank(T) 이고, rank는 dim(V) - nullity(T) 이다. 때문에 rank가 클수록 nullity는 작아지고, nullity가 작아질수록 rank는 커진다.




## 차원 정리의 증명

dim(V) = n, nullity(T) = k라 하고, N(T) 의 기저를 {$v_1, v_2, ... , v_k$} 라 하자.
N(T)의 정의는 선형 변환의 결과값이 0인 V의 원소들이므로, V의 subspace 들임을 알 수 있다.
replacement theorem의 따름 정리를 이용하여, subspace의 기저를 확장하여 그 subspace가 속한 vector space의 기저를 구할 수 있다.
따라서, V의 subspace 인 N(T)의 기저 {$\ v_1, v_2, ... , v_k \$}를 이용하여 V의 기저인 {$\ v_1, v_2, ... , v_n \$} 을 얻을 수 있다는 것이다.

위 정리와 동일한 세팅에서 $R(T) = span({T(v_1), T(v_2), ... , T(v_n)})$ 이므로, $S = \{T(v_{k+1}), T(v_{k+2}), ... , T(v_{n})\}$ 이 R(T)의 기저임을 보이면 rank가 n-k임을 보이게 되기 때문에
증명을 완료할 수 있다. 따라서 S가 R(T) 의 기저임을 보이기 위해서, 아래와 같은 2가지 내용을 보여야 한다.

1. span(S) = R(T)
2. S는 일차 독립이다.

1번을 먼저 보이기 위해서, 위에 적었던 R(T) = span({$T(v_1), T(v_2), ... , T(v_n)$}) 그대로 적어 보자. 여기서 $T(v_1), T(v_2), ... T(v_k)$ 은 N(T)의 기저로 가정한 부분이기 때문에
i=1, ... n 에 대하여 $T(v_i) = 0$ 이므로 아래와 같이 쓸 수 있다.

$$\begin{eqnarray*}
 R(T)&=& \text{span}({T(v_1), T(v_2), ... , T(v_n)}) \\
     &=& \text{span}({T(v_{k+1}), T(v_{k+2}), ... , T(v_n)}) \\
     &=& \text{span}(S)
\end{eqnarray*}$$

2번 S는 일차 독립임을 보이기 위해서 S의 선형결합으로 영 벡터를 표현해본다. 선형결합의 모든 계수가 0 일때만 영 벡터를 표현할 수 있으면 S는 일차 독립이라고 할 수 있다.
$\sum_{i=k+1}^n b_{i}v_{i}$를 어떤 한 벡터로 본다면, 이 벡터는 N(T)에 속해있는 것과 마찬가지 이므로 아래와 같이 쓸 수 있다.

$$T(\sum_{i=k+1}^n b_{i}v_{i}) = 0 \iff \sum_{i=k+1}^n b_iv_i \in N(T)$$

따라서, N(T)에 속해있는 한 벡터에 대해 kernel의 기저인 {$\ v_1, v_2, ... , v_k \$}의 선형결합으로 표현할 수 있는 것은 자명하고, R(T)의 기저인 S의 선형결합으로도 표현할 수 있다는 뜻이다.
이를 정리해서 아래와 같이 쓸 수 있다.

$$\sum_{i=1}^k c_{i}v_{i} = \sum_{i=k+1}^n b_{i}v_{i} \iff \sum_{i=k+1}^n b_{i}v_{i} + \sum_{i=1}^k -c_{i}v_{i} = 0  $$

N(T)의 기저의 선형결합과 R(T)의 기저의 선형결합으로 영 벡터를 표현헸지만, 이는 곧 V의 기저로 영 벡터를 표현한 것과 똑같다.
따라서 모든 $b_i, c_i$는 0이고, rank(T) = n-k이다.

nullity와 rank, 그리고 차원정리는 선형대수학을 배우면서 계속 언급되는 개념들이므로, 너무 중요해서 리마인드 하는 겸 포스팅을 해보았다. 후!

>Reference
>\- 스티븐 H.프리드버그, 아놀드 J.인셀, 로렌스 E, 스펜스, **『**프리드버그 선형대수학 5판**』**,한빛 아카데미(2020)
