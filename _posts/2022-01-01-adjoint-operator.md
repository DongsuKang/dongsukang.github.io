---
title:  "선형대수의 수반 연산자(adjoint operator)에 대해 알아보자"
excerpt: "선형대수의 수반 연산자(adjoint operator) 이 무엇인지, 존재를 어떻게 증명하는지를 알아보자"

categories:
  - Linear Algebra

toc: true
toc_sticky: true

use_math : true
comments : true
image : true
sitemap :
changefreq : daily
date: 2022-01-01
last_modified_at: 2022-01-01
---
## 들어가기 전에..
스터디 원들의 도움으로 어느 덧 프리드버그 선형대수의 교재 마지막장 6장에 들어서게
되었다. 실제로 마지막 장은 아니지만, 교재에서 7장을  further study로 언급했기에,
이전 선대 회차에서는 7장에 대해 하지 않았기 때문에 6장까지 하게 되었다.
기존에는 강의를 따라가는 학생의 입장이었다면, 지금은 격주로 번갈아가면서 학생과
세미나를 주도하는 입장을 되어봤다. 확실히 다른 사람에게 아는 것을 전달하기 위해서는
가르치는 내용에 대해 보이는 것보다 훨씬 더 잘 이해해야 한다는 사실을 깨달았다.

6장은 내적 공간에서 사용할 수 있는 함수 '내적'으로 새로운 operator 들을 배우고, 이
operator 들의 성질을 이용해 최종적으로 스펙트럼 정리에 대해 배우게 된다.
6장의 내용은 앞에서 배웠던 벡터공간의 정의부터 대각화의 내용까지를 전부 아우르고 있으며
그래서 상당히 어렵지만, 5장까지의 내용을 잘 알고 있다면, 쏠쏠한 재미를 볼 수 있는
부분이기도 하다.

평소보다 사설이 길었는데, 오늘은 6장에서 새로이 등장하는 linear operator의 종류 중에
이해하기가 가장 어려웠던 adjoin operator 에 대해 오늘 진행한 세미나를 토대로
정리를 해보고자 한다.

## 수반 연산자(adjoint operator)이란?

교재에서의 정의는 아래와 같다.  
 > **정의** 유한 차원 내적공간 V와 선형 연산자 $T : V \rightarrow V$ 를 생각해보자. V의 임의의 벡터 $\mathbf{x, y}$ 에 대하여 $\langle T(\mathbf{x}), \mathbf{y} \rangle = \langle \mathbf{x}, T^{\ast}(\mathbf{y}) \rangle$ 인 함수 $T^{\ast} : V \rightarrow V$ 가 유일하게 존재한다. 특히, $T^\ast$ 는 선형 변환이다.

여기에서의 핵심은 T의 adjoint operator 가 내적에서 아래와 같은 성질을 만족한다는 것이다.

$$\langle T(\mathbf{x}), \mathbf{y} \rangle = \langle\mathbf{x}, T^{\ast}(\mathbf{y}) \rangle$$

위의 성질, 그 유명한, 최소 제곱법의 증명에서도 굉장히 유용하게 사용이 된다.




## 내적 공간에서 실수 공간으로 가는 함수는 모두 내적 꼴로 표현될 수 있다.

adjoin operator 의 존재를 증명하기 전에, 정의역을 내적공간으로 하고, 치역을 실수 공간으로 하는 함수의 형태에 대해 먼저 정리할 필요가 있다. 즉, 이러한 함수를 $g : V \rightarrow F$ 라고 했을 때, 함수 g는 선형이면서, 항상 $\langle \mathbf{x, y} \rangle$와 같은 꼴이다. 그 내용이 아래 정리의 내용과 같다.

 > **정의** 유한차원 F-내적공간 V와 선형변환 $g : V \rightarrow F$를 생각하자. 모든 $\mathbf{x} \in V$ 에 대하여 $g(\mathbf{x}) = \langle \mathbf{x, y} \rangle$ 를 만족하는 벡터 $\mathbf{y} \in V$ 가 유일하게 존재한다.

증명에서는 V의 정규직교기저 $\mathfrak{B} = \\{\mathbf{v_1}, \ldots, \mathbf{v_n} \\}$ 를 가정하고, 벡터 y의 형태를 $\sum_{i=1}^{n}\overline{g(\mathbf{v_i})}\mathbf{v_i}$ 로 가정한다.

그리고 새로이 함수 V에서 F로 가는 함수 h 를 만들고, h의 정의를 $\langle \mathbf{x}, \mathbf{y} \rangle$ 라 정의한다. 이 때, 정규직교기저의 j 번째 벡터를 기준으로 $h(\mathbf{v_j} = g(\mathbf{v_j})$ 가 같음을 보인다.

즉, basis에 대해서 함숫값이 같음을 보인 것이므로, 이전에 작성한 [포스팅](https://dongsukang.github.io/linear%20algebra/linear-extention-thorem/) 과 같이 linear extention thorem 에 의해 g = h 인 것을 보인다. (벡터 y의 유일성 증명은 생략)

여기에서의 포인트는

1. 위에서 언급했던 것과 같이, 내적 공간에서 실수공간으로 가는 선형변환의 형태는 사실 모두 내적 꼴이라는 점이다.

2. 함수 g를 잡을 때마다, $g(\mathbf{x}) = \langle \mathbf{x}, \mathbf{y} \rangle$ 를 만족하는 $\mathbf{y}$가 유일하게 존재하므로, 함수 g는 V와 F 사이의 bijective function 이다.

## 다시 adjoint의 정의를 보자

> **정의** 유한 차원 내적공간 V와 선형 연산자 $T : V \rightarrow V$ 를 생각해보자. V의 임의의 벡터 $\mathbf{x, y}$ 에 대하여 $\langle T(\mathbf{x}), \mathbf{y} \rangle = \langle \mathbf{x}, T^{\ast}(\mathbf{y}) \rangle$ 인 함수 $T^{\ast} : V \rightarrow V$ 가 유일하게 존재한다. 특히, $T^\ast$ 는 선형 변환이다.

V의 임의의 벡터 y를 고정하고, 모든 벡터 x에 대해서 함수 $g : V \rightarrow F$ 를 $g(\mathbf{x}) = \langle T(\mathbf{x}), \mathbf{y} \rangle$ 라고 정의한다.

함수 g가 선형인지 체크해보면 쉽게 선형임을 알 수 있다.

(여기서부터 좀 헷갈릴 수 있는 부분) 바로 위 섹션의 정리에서는 내적공간에서 실수공간으로 가는 선형 변환의 형태가 모두 $g(\mathbf{x}) = \langle \mathbf{x}, \mathbf{y'} \rangle$ 이렇다고 얘기한 바 있다. **(갑자기 y'이 등장한 이유는, 윗 섹션에서 사용한 벡터 y와 현재 사용하고 있는 벡터 y가 서로 다른 것임을 보이기 위해서다. 즉, 그냥 표기가 다른 거다)**

그런데, 이번 adjoint의 존재성에 대한 증명에서는 우리는 함수 g를 아래와 같이 정의 했다.

$$g(\mathbf{x}) = \langle T(\mathbf{x}), \mathbf{y} \rangle$$

내적의 첫 부분이 $\mathbf{x}$와 $T(\mathbf{x})$ 로 조금 다른데, 우선 바로 위 섹션에서의 정리에 의하면 아래와 같은 등식이 성립해야 한다.

 $$\langle T(\mathbf{x}), \mathbf{y} \rangle = \langle \mathbf{x}, \mathbf{y'} \rangle$$

 이 때 함수 $T^\ast : V \rightarrow V$ 를 $T^\ast(\mathbf{y}) = \mathbf{y'}$ 로 정의하면, $\langle T(\mathbf{x}), \mathbf{y} \rangle = \langle \mathbf{x}, T^{\ast}(\mathbf{y}) \rangle$ 를 얻을 수 있다.

 1. 정리해보면....(귀찮으니 latex 생략) 정의역을 내적공간으로 하고, 치역을 실수 공간으로 하는 함수 g는 모두 g(x) = <x, y'> 와 같은 꼴이고, 심지어 y'도 유일하다. 여기까지가 바로 위의 섹션에서 정리했던 내용.

 2. 그리고, 이번에는 정의역과 치역을 이전과 똑같이, 각각 내적공간과 실수 공간으로 하는 함수 g를 정의하는데 이번에는 <T(x), y>로 가정한다.

 3. 1번의 내용에 의하면 <T(x), y>도 결국 <x, y'>의 형태와 같아야 한다.

 4. 이 때, T의 adjoint operator에 y를 evaluate한 형태를 y'으로 정의한 것이다. (즉, $T^\ast(\mathbf{y}) = \mathbf{y'}$)

 5. 최종적으로, adjoint operator의 정의에 맞게, <T(x), y> = <x, T\*(y)> 를 만족하게 되면서, T\*가 있음을 보이게 되는 것이다.

이렇게 adjoint operator를 보이게 되고, 교재에서는 T\*의 선형성과 T\*의 유일성까지 증명을 하지만, 이부분은 그렇게 어렵게 느껴지지 않았으므로 생략한다.

## 글을 마치며...

사실 진짜 어렵게 느껴졌던 부분은 이거다. 이전까지의 선대에서는 흐름을 따라 쭉 가다보면, 새로운 증명을 짠 하고 찾아냈다. 즉, 길을 따라 가다보니 새로운 무언가를 발견한 것이다. 물론, 그 새로운 무언가가 있는 줄 알고 따라 간 것은 아니다.

그런데, adjoint opeartor의 느낌은....뭐랄까...이런게 있는 건 알겠고, 그래서 그걸 얻으려면 어떤 길을 어떻게 따라가지를 끼워 맞춘 느낌이었다. 원하는 것을 얻기 위해 수학적으로 말이 되게 세팅한 느낌.
그래서 더 어렵게 느껴지기도 했지만, 그래서 이해하는 재미도 있었던 것 같다.
(이해해 많은 도움을 준 수학 천재 신의야, 고마워!)

>Reference
>\- 스티븐 H.프리드버그, 아놀드 J.인셀, 로렌스 E, 스펜스, **『**프리드버그 선형대수학 5판**』**,한빛 아카데미(2020)
