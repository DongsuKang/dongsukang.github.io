---
title:  "Linear Extension Theorem"
excerpt: "선형대수의 linear extension theorem에 대해 공부해보자."

categories:
  - Linear Algebra

toc: true
toc_sticky: true

use_math : true
comments : true

sitemap :
changefreq : weekly

date: 2020-12-28
last_modified_at: 2020-12-28
---

## 들어가기 전에
여담이지만, 선형대수학을 처음 공부할 때만해도, '그래서 어쩌라는 거지...?'라는 생각을 많이 했다. 가령, 벡터 공간이 되기 위해서는 덧셈에 대해 교환법칙이 성립해야 한다. 그래서 어쩌라는거지...? 이런 식이다. 책을 2회독할 때쯤엔 같은 문장이 다르게 보이기 시작했는데, linear extension theorem 또한 그렇다. 사실 증명의 내용은 궁금하면 찾아볼 수 있지만, 책에 적혀 있지 않지만 깨달은 의미를 남기기 위해 이 포스팅을 작성한다.

## Linear Extension Theorem이란?

정리의 내용은 아래와 같다

> **Thm** Let V and W be vector spaces over $F$, and suppose that $\{\mathbf{v_1, v_2, ... , v_n}\}$ is a basis for $V$. For $\mathbf{w_1, w_2, ..., w_n} \in W$, there exists exactly one linear transformation $T : V \to W$ such that $T(v_i) = w_i$ for $i = 1, 2, ... , n.$

증명의 시작 전에 먼저 아래와 같이 기본적인 세팅을 하려 한다.

$$\begin{align}
\mathbf{x} \in V, \mathbf{x} = \sum_{i=1}^n a_i\mathbf{v_i}
 \end{align}$$

그리고, W의 벡터 중 $T(\mathbf{x})$와 대응되며, $\mathbf{w_i}$의 선형결합으로 표현되는 벡터를 찾아 매핑시켜준다.
수식으로 정리하면 아래와 같다.  

$$\begin{align}
T(\mathbf{x}) = \sum_{i=1}^n a_i\mathbf{w_i}
\end{align}
$$

위 정리를 증명하기 위해서는 총 3가지를 보여야 한다.

1. T가 선형 변환이라고 하는데, 진짜 선형 변환인가?(T가 linear임을 증명)
2. $T(v_i) = w_i$를 만족하는 선형 변환 T가 존재한다고 주장했는데, 진짜 존재 하는가?
3. 선형 변환 T가 유일하다고 주장했는데, 진짜 유일한가?

일부러 순서대로 적은 것이긴 하지만, T가 선형 변환임이 먼저 증명되어야, 선형 변환의 linear함을 이용해 뒤의 내용들을 증명할 수 있기 때문에, 증명의 순서는 1 - 2 - 3이다.

## 1.선형성(linearity)

T가 linear하다는 주장은 곧 $T(c\mathbf{x + y}) = cT(\mathbf{x}) + T(\mathbf{y})$와 동치이다.
$\mathbf{u, v} \in V, d \in \mathbb{F}$라고 가정하면, $\mathbf{u, v}$는 각각 V의 기저의 선형결합으로 표현할 수 있다.

$$\mathbf{u} = \sum_{i=1}^n b_i\mathbf{v_i}, \mathbf{v} = \sum_{i=1}^n c_i\mathbf{v_i}, \ b_i, c_i \text{는 모두 unique scalar} $$

따라서 $T(d\mathbf{u + v})$는 다음과 같이 쓸 수 있다.

$$T(d\mathbf{u + v}) = T(d\sum_{i=1}^n b_i\mathbf{v_i} + \sum_{i=1}^n c_i\mathbf{v_i}) = T(\sum_{i=1}^n (db_i + c_i)\mathbf{v_i}) = \sum_{i=1}^n (db_i + c_i)\mathbf{w_i}=d\sum_{i=1}^n b_i\mathbf{w_i} + \sum_{i=1}^n c_i\mathbf{w_i} = dT(\mathbf{u}) + T(\mathbf{v}) $$

위의 식을 통해 T는 linear함을 알 수 있다.

## 2.존재성(existing)

책에서는 clearly하게 라고 적어놓고 그냥 넘어가는 부분인데, 이해하는데 가장 어려웠던 부분이다. 주변의 훌륭한 친구들 덕분에 이해할 수 있었다.

사실 이 부분은 증명의 (1)과 (2)의 수식들을 설정할 때 이러한 선형 변환임을 감안하고 세팅을 해줬기에 책에서 적혀있는 대로 'clear'하다고 이야기할 수 있다.

무슨 이야기인고 하니, 정리에서 주장하는 바와 같이 $T(v_i) = w_i$를 만족하는 선형 변환을 의도적으로 찾아 (1), (2)와 같은 설정을 해주었다는 뜻이다.
때문에 (2)의 식에 $\mathbf{x}$ 자리에 $\mathbf{v_i}$를 대입할 경우, $T(\mathbf{v_i}) = \mathbf{w_i}$가 성립되면서 선형사상 T의 존재성이 증명이 된다.


## 3. 유일성(uniqueness)

T가 유일하지 않고, T 이외에 $U:V \to W, \ U(\mathbf{v_i}) = \mathbf{w_i}$를 만족하는 선형 변환 U가 존재한다고 가정해보자.
아래와 같은 관계식을 얻을 수 있다.

$$\mathbf{x} \in V, U(\mathbf{x}) = \sum_{i=1}^na_i U(\mathbf{v_i}) = \sum_{i=1}^n a_i\mathbf{w_i} = T(\mathbf{x})$$

따라서, 정리에서 주장한 T의 선형성(linearity), $T(\mathbf{v_i}) = \mathbf{w_i}$를 만족하는 T의 존재성(exist) 그리고 마지막으로 이러한 T는 유일하다는 유일성(uniqueness)까지 증명하며 주장이 마무리가 된다.

## Linear Extension Theorem의 의미

선형 변환은 원래 집합 간 정의되는 함수 이므로, 정의역의 임의의 원소에 대해 함숫값에 대한 정의가 필요하다. 예를 들어서 정의역과 치역의 원소가 모두 1부터 10까지인 함수가 있다고 할 때, 정의역의 1의 함숫값은 치역의 2이고 이런 식이 되야 한다. 하지만 linear extension thorem을 사용할 경우, 정의역의 일부 원소(=여기서는 기저)의 함숫값만 결정되면, 정의역의 나머지 원소들 또한 함숫값이 자동으로 결정되고, 이렇게 함숫값이 결정되면서 이 함수는 선형 변환으로 정의 내릴 수 있게 되는 것이다.

요약해보면 이 정리를 알고 있으면, 정의역의 기저의 함숫값만 알고 있어도, 이 함수가 선형변환이고, 심지어 유일하다고도 얘기할 수 있다. 벡터 공간의 성질과 선형 변환의 선형성을 잘 이용한 덕분이다. 그리고 이 정리는 선형 변환의 집합과 행렬의 집합에 일대일 대응 함수가 존재하다는 **선형대수의 기본정리**의 증명에도 활용된다.





>Reference
>\- 스티븐 H.프리드버그, 아놀드 J.인셀, 로렌스 E, 스펜스, 『프리드버그 선형대수학 5판』,한빛 아카데미(2020)
