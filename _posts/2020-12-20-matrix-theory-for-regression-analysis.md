---
title:  "회귀분석을 위한 행렬이론"
excerpt: "회귀분석을 공부할 때 필요한 행렬이론을 공부 해보자."

categories:
  - Statistics

toc: true
toc_sticky: true

use_math : true
comments : true

sitemap :
changefreq : weekly
date: 2020-12-20
last_modified_at: 2020-12-20
---

\- 아래 내용은 부산대학교 김충락 교수님의 13년 강의를 KOCW에서 보고 정리한 내용입니다.

(강의 링크 : www.kocw.net/home/search/kemView.do?kemId=703282&ar=link\_gil)

\- 공부 내용을 정리하기 위해 작성하며, 글 중간 중간 제가 개인적으로 추가 내용을 작성한 것이 있는데 당연히 잘못 되었을 가능성이 있습니다. 틀린 부분이 보이시면, 말씀해주시면 감사하겠습니다.

---

### Properties of matrix

- $rank(AB) \le min(rank(A), rank(B))$

위 내용은 선형대수학을 이용하면 증명할 수 있다. 먼저 유한 차원 벡터공간 $V, W, Z$ 사이에 정의된 선형 변환 $T : V \\to W, U : W \\to Z$와 행렬 곱 AB를 정의하는 두 행렬 A, B가 있다고 하자. 이 때, $rank(UT) \le rank(U)$ 가 성립되는데, 그 증명은 아래와 같다.

선형 변환 T의 image인 $R(T)$는 $W$의 subset 이므로 다음이 성립한다.

$R(UT) = UT(V) = U(T(V)) = U(R(T)) \subseteq U(W) = R(U)$

(위 식에서 $R$은 range)

따라서 $rank(UT) = dim(R(UT)) \le dim(R(U)) = rank(U)$ 이다.

위 내용을 이용하면 $rank(AB) \le rank(A)$ 임도 증명할 수 있는데, 그 증명은 아래와 같다.

$$rank(AB) = rank(L_{AB}) = rank(L_{A}L_{B}) \le rank(L_{A}) = rank(A)$$

다시 위의 두 명제를 이용하면, $rank(AB) \le rank(B)$ 임을 증명할 수 있다.

$$rank(AB) = rank((AB)^t) = rank(B^tA^t) \le rank(B^t) = rank(B)$$

위 내용들을 종합해보면, $rank(AB) \\le rank(AB)$와 $rank(AB) \\le (B)$이 성립된다. 예를 들어 A의 rank가 3이고, B의 rank가 2라고 해보자. $rank(AB)$는 $rank(A)$보다 작거나 같고, $rank(B)$보다도 작거나 같아야 하는데, $rank(AB)$ 가 A의 rank인 3이라면, 이는 $rank(AB) \\le (B)$를 위반하게 된다. 따라서 $rank(AB)$는 $rank(A)$와 $rank(B)$ 중 작은 수를 취할 수 밖에 없고$rank(AB) = min(rank(A), rank(B))$ 가 성립된다.

- n \* n 행렬 A가 non-singular 일 경우, rank(A) = n 이다. A가 singular 일 경우, rank(A) < n 이다.

행렬 A가 non singular라는 의미는 곧 행렬 A가 n \* n 가역행렬임을 의미한다. n \* n 행렬이 가역이기 위한 필요충분조건은 행렬의 랭크가 n 인 것이다. 이를 증명하는 방법 중 하나는 비둘기 집의 원리이다. 행렬 A에 대응하는 선형변환을 생각해보면, 이 선형변환의 정의역과 치역의 dimension이 n으로 같음을 알 수 있다. 따라서 비둘기 집의 원리에 의해, 이 선형 변환의 nullity는 0이므로, dimension thorem에 의해 이는 곧 정의역의 dimension과 rank가 같음을 의미한다. 

행렬 A가 비특이행렬(=singular matrix)라는 것은, 행렬 A의 역행렬이 존재하지 않음을 의미한다.  n \* n 행렬이 비가역이므로 행렬의 랭크는 n보다 작을 수 밖에 없다. (이렇게 마무리 되면 안 될 것 같은데 찝찝하다)


- 행렬 B가 non-singular 일 때, $rank(A) = rank(BA)$ 이다.

모든 가역 행렬은 기본 행렬의 곱으로 나타낼 수 있는데, 어떤 행렬에 기본 행렬을 곱해도 그 행렬의 rank는 변하지 않는다.


- 만약 행렬 A, G가 $AGA = A$ 를 만족하면, $rank(A) = rank(GA)$ 이다.


- 행렬 $A : m*n_1$, 행렬 $B : m * n_2$ 라고 하자. $A\|B: m * (n_1 + n_2)$ 이고, 이를 augmented matrix(첨가 행렬) 이라고 한다. 이 때, $rank(A\|B) \le rank(A) + rank(B)$ 이다.

정확한 증명은 생각나지 않지만, 이렇게 생각해보았다. 먼저 $rank(A\|B)$와 $rank(A) + (B)$가 같은 경우를 생각해보자. 첨가 행렬이 결국 행렬 A 옆에 행렬 B의 컬럼을 갖다 붙이는 형태인데, rank를 따지기 위해서 이 때 주목해야 할 것은 갖다 붙히고 나서 rank가 유지 되는지이다. 아래 2가지 경우를 생각해 볼 수 있다.



>1. 추가된 행렬 B의 컬럼으로 인해 $rank(A\|B)$가 줄어들지 않는 경우 : $rank(A\|B) = rank(A) + rank(B)$를 만족
>
>2. 추가된 행렬 B의 컬럼으로 인해 $rank(A\|B)$가 줄어드는 경우 : $rank(A\|B) < rank(A) + rank(B)$


위 2가지를 고려해봤을 때, $rank(A\|B) \le rank(A) + rank(B)$ 임을 알 수 있다.



- 행렬 A, B가 있을 때, $rank(A+B) \le rank(A\|B) \le rank(A) + rank(B)$ 이다.

$rank(A\|B) \le rank(A) + rank(B)$에 대한 얘기는 위 5번에서 했으므로 우측의 $rank(A+B) \le rank(A\|B)$만 얘기하면 된다. 이 역시 정확한 증명은 모르겠으나, 생각해보자. 행렬 A와 B를 모두 n * n 행렬이라 하면, $A+B$는 n \* n 행렬이지만 $A\|B$는 n * 2n 행렬이다. 즉, $rank(A\|B)$은 n부터 2n까지 가능하며 $rank(A+B)$는 full rank일 경우 n이고 그 보다 작을 수 있다. 



- 행렬 A, B가 n * n 일 때, $rank(AB) \ge rank(A) + rank(B) - n$ 이다.



- A가 idempotent(멱등행렬) 일 경우, $rank(I-A) = n-rank(A)$ 이다.


- $rank(A) = rank(A^t) = rank(AA^t) = rank(A^tA)$

첫 번째 등호의 성립은 아래와 같이 이해할 수 있다.랭크가 $r$ 인 $m x n$ 행렬 A는 유한 번의 기본 열 연산을 사용하여 행렬 A를 다음과 같은 꼴로 바꿀 수 있다.

$$D = \begin{pmatrix} I_r & O_1 \\ O_2 & O_3 \end{pmatrix} = BAC,\ where\ O_1,\ O_2,\ O_3\ is\ zero\ matrix $$

이 때, B, C는 가역행렬이다. 행렬 D를 구하기 위해 유한 번의 기본 열 연산을 적용했다는 것은 곧 행렬 A에 기본 행렬 $E\_pE\_{p-1} \\cdots E\_2E\_1$을 A의 앞 뒤로 곱했다는 의미인데, A의 앞 뒤로 적용된 기본 행렬들을 모두퉁쳐서 앞의 기본행렬의 곱들은 B로, 뒤의 기본 행렬의 곱들은 C로 표현할 수 있고, 기본행렬끼리의 곱은 기본 행렬이며, 모든 기본 행렬은 가역 행렬이므로 B, C도 가역행렬임을 알 수 있다.

D의 전치 행렬을 구하면 아래와 같이 쓸 수 있다.

$$D^t=(BAC)^t=C^tA^tB^t$$

B와 C는 가역 행렬이므로, $B^t$와 $C^t$도 가역행렬임을 알 수 있다. 어떤 행렬의 앞뒤에 가역행렬을 곱한다해도, 그 행렬의 랭크는 변하지 않는데, 이는 현재 얘기하고 있는 행렬 A, B, C, D를 이용하여 아래와 같이 쓸 수 있다.

$$rank(A^t) = rank(C^tA^tB^t) = rank(D^t)$$

이 때, $rank(A)$를 r이라고 하면, 우리는 행렬 D의 형태를 알고 있으므로 아래와 같은 결론을 얻을 수 있다.

$$rank(A^t) = rank(D^t) = r = rank(A)$$

따라서 $rank(A) = rank(A^t)$ 임을 알 수 있다.   

두 번째 등호의 증명은 맞는지 잘 모르겠으나 생각 나는대로 적어보면

$A^t$를 행렬 B라고 보면, 위 1번의 $rank(AB) \\le min(rank(A), rank(B))$를 적용해볼 수 있을 것 같다. $rank(A) = rank(B) = rank(A^t)$이므로, $rank(A^t) = rank(AA^t)$라 할 수 있겠다. 마지막 등호도 동일하게 순서만 바꿔서 적용하면 될 것 같다. 

---

>Reference
>\- 스티븐 H.프리드버그, 아놀드 J.인셀, 로렌스 E, 스펜스, **『**프리드버그 선형대수학 5판**』**,한빛 아카데미(2020)
