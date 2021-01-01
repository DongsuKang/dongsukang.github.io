---
title:  "선형대수의 Rank Theorem 정리"
excerpt: "선형대수의 Rank Theorem 에 대해 공부해보자."

categories:
  - Linear Algebra

toc: true
toc_sticky: true

use_math : true
comments : true

sitemap :
changefreq : weekly

date: 2020-12-31
last_modified_at: 2020-12-31
---



## Rank Theorem이란?

Rank theorem은 임의의 행렬의 row과 column은 차원이 같은 부분공간을 생성한다는 뜻이다. **이는 결국 A의 row rank와 column rank가 같다는 것을 의미한다.** 때문에 rank theorem의 의미는 명확한데 행렬의 랭크는 row를 기준으로 하든 column을 기준으로 하든 상관이 없다는 뜻이다. 어차피 그 둘은 항상 같기 때문이다.

여기서 과거의 나였다면 2 가지 납득이 가지 않을 만한 포인트가 있다.

1. 행렬의 랭크에는 row rank와 column rank 2가지가 있다고?
2. 서로 다른 이름을 가진 2개의 rank가 항상 같은 값을 가진다고 얘기하는 rank theorem 자체를 아마 이해하지 못했을 것이다.

1번에 대한 얘기는, 첫 문장에서부터 시작할 수 있다. '행렬의 행과 열이 각각 부분공간을 생성하는구나'.
직관적으로 row rank는 행이 생성하는 공간의 차원을, column rank는 열이 생성하는 공간이라고 느낄 수 있다. 조금 더 자세하게 얘기해보면...

## 행렬의 row와 column이 생성하는 부분 공간

> **Theorem** 임의의 행렬의 랭크는 일차독립인 열의 최대 개수와 같다. 행렬의 랭크는 그 열에 의해 생성된 부분공간의 차원이다.

행렬 A가 m * n 형태의 행렬이라면, $rank(A) = rank(L_A) = dim(R(L_A))$가 성립한다. 행렬 A의 정의역에 해당하는 $\mathbb{F}^n$의 표준 순서 기저를 $\mathfrak{B}$ 라고 하면,
span$(\mathfrak{B})$가 $L_A$의 image와 같은데, 수식으로 표현하면 아래와 같다.

$$R(L_A) = \text{span}L_A(\mathfrak{B}) = \text{span} \{ L_A(\mathbf{e_1}), L_A(\mathbf{e_2}), \cdots, L_A(\mathbf{e_n}) \}$$

이 때, 행렬 A의 j번째 column을 $a_j$라 하면, left multiplication transformation의 정의에 따라 $L_A(\mathbf{e_j}) = A\mathbf{e_j} = a_j$ 임을 알 수 있다.

$$rank(A) = dim(R(L_A)) = dim(\text{span} \{ a_1, a_2, \cdots, a_n) \})$$

따라서 A의 column을 벡터로 span 하면 치역의 부분공간을 생성한다.  

위와 비슷하게 $A^t$를 생각해보면, $rank(A) = rank(A^t)$임을 알 수 있는데, 이러한 row와 column의 벡터들이 만드는 부분공간들과 관련된
notation들을 정리해보면 아래와 같이 쓸 수 있다.

$$
A \in M_{n \times n}(\mathbb{R}),
A = \begin{pmatrix} \mathbf{r_1} \\ \vdots \\ \mathbf{r_n} \\ \end{pmatrix} =
\{\mathbf{c_1}, \cdots, \mathbf{c_n} \} \\
\begin{array}{rcl}
\mathbb{R}(A) &:=& \text{span}\{\mathbf{r_1, \cdots, r_n}\} : \text{row space of A} \\
\mathbb{C}(A) &:=& \text{span}\{\mathbf{c_1, \cdots, c_n}\} : \text{column space of A} \\
\mathbb{N}(A) &:=& \text{span}\{\mathbf{x} \in \mathbb{R}^n : A\mathbf{x} = \mathbf{0}\} : \text{null space of A}
\end{array}
$$

위 notation이 얘기하는 바는, 임의의 n * n 행렬 A는 A의 row들을 basis로 하는 row space로 볼 수도 있고, 동시에 column들을 basis로 하는 column space라고도 볼수도 있다는 뜻이다. 때문에 행렬의 row와 column이 각각 행렬 A의 부분 공간을 생성한다고 말할 수 있다. 그리고 마지막으로 null space가 뜻하는 바는 행렬 A에 대응하는 선형 변환에서 kernel에 해당한다. (선형 대수의 기본정리 참고 자료 [클릭](https://seanie12.github.io/blog/linear%20algrbra/fudamental-theorem-of-linear-algebra/))

## row와 column이 생성하는 부분 공간의 차원이 항상 같다?

행렬 A가 m * n 행렬이라 하자.

행렬 A에 대응하는 left multiplication transformation을 생각해보면 row space와 null space가 $\mathbb{R}^n$의, column space가 $\mathbb{R}^m$의 subspace 임을 알 수 있다. 위 단락에서 얘기한 바와 같이, null space가 $L_A$의 kernel을 의미한다면, column space 는 아래와 수식과 같은 과정을 통해 $L_A$의 image 와 같다.

$$
\begin{array}{rcl}
\mathbb{C}(A) &=& \text{span}\{c_1, \cdots, c_n \} \\
              &=& \{A\mathbf{x} : \mathbf{x} \in \mathbb{R}^n\} \\
              &=& \{L_A\mathbf{x} : \mathbf{x} \in \mathbb{R}^n\} \\
              &=& \text{image}L_A
\end{array} $$

행렬 A에 대응하는 $L_A$는 선형변환이고, 선형 변환의 정의역의 차원은 rank와 nullity의 관계로 설명이 가능하다는 것을 이전 포스팅에서 증명한 바 있다. ([차원 정리 이전 포스팅 참고](https://dongsukang.github.io/linear%20algebra/dimension-theorem/))

따라서 row와 column이 생성하는 부분 공간들의 차원이 같다는 것은 아래와 동치이다.

$$\text{nullity}(L_A) + \text{rank}(L_A) = n \iff \text{nullity}(L_A) + (\text{column rank of A}) = n$$

때문에, $L_A$의 nullity와 A의 row rank 의 합이 n임을 보이면, A의 row rank와 column rank가 같다는 것을 보이게 된다.

이를 보이기 위해 행렬 A의 행간소사다리꼴을 생각해보자. 역시나 이전 포스팅에서 다룬 행간소사다리꼴의 내용 중에 임의의 행렬은 대응하는 유일한 행간소사다리꼴을 가지고 있다는 사실을 적은 바 있다.(증명은 없지만, [행간소사다리꼴 관련 이전 포스팅 참고](https://dongsukang.github.io/linear%20algebra/reduced-row-echelon-form/))

예를 들어, 행렬 A가 4 * 5 행렬이고, 행렬 A의 행간소사다리꼴 형태를 아래 행렬 R이라 하자.

$$R =
\begin{pmatrix}
1 & 0 & 2 & 0 & 3 \\
0 & 1 & 2 & 0 & 1 \\
0 & 0 & 0 & 1 & 2 \\
0 & 0 & 0 & 0 & 0 \ \end{pmatrix}
$$

행렬 R에 대응하는 $L_R$의 nullity는 $R\mathbf{x=0}$의 해집합의 차원인데, 실제로 구해 보면 위 행렬 R의 해집합의 차원은 2이다. 그리고 R의 row rank를 살펴 보면 (바로 위의 단락에서 적은 바와 같이)각 row 별로 첫 번째 원소가 1인 row의 수, 즉, 첫 번째, 두 번째, 세 번째 row가 서로 선형 독립이므로 R의 row rank는 3이다. 행렬 R의 정의역의 차원은 5이므로, 2 + 3 = 5 이므로 row rank와 column rank가 같음이 증명된다.  

정리해보면, 임의의 행렬 A에 대응하는 행간소사다리꼴 R과, 이에 대응하는 $L_R$ 을 생각해서, $L_R$의 nullity와 행렬 R의 row rank의 합을 차원 정리를 통해 정의역의 차원과 같음을 보임으로써 row rank와 column rank의 같음을 증명하였다.

정리는 다 증명한 것 같은데 무언가...시간 나면 다시 한 번 봐야겠다.


>Reference
>\- 스티븐 H.프리드버그, 아놀드 J.인셀, 로렌스 E, 스펜스, 『프리드버그 선형대수학 5판』,한빛 아카데미(2020)
