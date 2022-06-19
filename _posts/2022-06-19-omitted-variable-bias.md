---
title:  "회귀 모형에서의 OVB(Omitted Variable Bias)에 대해 알아보자"
excerpt: "OVB는 무엇이고, 어떻게 확인할 수 있을지 알아보자"

categories:
  - Causal Inference
  - Regression 
  - Statistics

toc: true
toc_sticky: true

use_math : true
comments : true
image : true
sitemap :
changefreq : daily
date: 2022-06-19
last_modified_at: 2022-06-19
---

\- 아래 내용은 책 '고수들의 계량경제학' 중 2장 회귀 분석 파트를 읽고 정리한 내용입니다.

## 배경 
- 회귀분석을 이용해 어떠한 현상의 인과를 추론하고자 할 때, 통제 해야 하는 변수를 회귀 모형에 포함시켜야 한다는 사실을 알고 있다. 
- 이는 내생성(endogenity)의 존재 때문인데, 여기서 내생성이 있다는 것의 의미는 회귀 모형에서 원인 변수와 잔차의 상관성이 있다는 의미이다. 
- 하지만, 내생성의 존재가 추론하고자 하는 효과에 어느 정도 영향을 미치는지 어떻게 설명할 수 있을까? 
    - 만약에 차이가 존재하긴 하나, 큰 차이가 존재하지 않는다면 어떻게 해야 할까?
- 이 때 OVB 를 통해, 우리는 통제해야 하는 변수가 누락 되었을 때 처치 효과에 끼치는 영향에 대해 설명할 수 있다.

## OVB(Omitted Variable Bias) 란?
- omitted variable 은 한국어로 하면 '누락 변수' 이다.
    - 이는 회귀 모형에서 내생성이 존재하는 경우, 내생성을 없애기 위해 변수에 포함시켰어야 했는데 포함시키지 않은 변수를 의미한다.
    - 즉, 포함 시켜서 내생성이 없도록 만들어주어야 했는데, 그렇지 않아서 '누락' 됐다는 의미로 해석할 수 있다. 
- OVB 를 설명하기 위해 책에서는 long regression 과 short regression 을 설명한다. 
- long, short regression 을 설명하기 위한 상황 설정
    - 사립, 공립 대학교 중 어떤 대학교를 가는 것이 소득에 영향을 얼마나 끼치는지를 파악한다고 가정해보자. 
        - 이 때, 처치 변수는 사립 또는 공립 대학교 여부를 더미 변수로 만들고, 결과 변수를 소득이라고 볼 수 있다. 
    - $A_i$를 임의의 누락변수라고 하면 long regression 의 회귀 모형은 아래와 같다. 
    $$\begin{align} 
    Y_i = \alpha^l + \beta^l P_i + \gamma A_i + e^l_i \\
    \end{align}$$
        - 여기서 $\alpha$ 는 절편, $\beta$는 처치 변수의 계수, $P_i$는 처치 변수, $\gamma$ 는 누락 변수의 계수, $e^l_i$의 잔차이다.
    - short regression 의 회귀 모형은 아래와 같다. 
    $$\begin{align} Y_i = \alpha^s + \beta^s P_i + e^s_i \end{align} \\ $$
    - 윗 첨자에 있는 l 과 s 의 차이는, 각각 long, short regression 의 계수라는 의미이다.
    - 만약 $\beta^s$ 가 20000이고, $\beta^l$ 가 10000이라면, 20000-10000만큼의 차이가 바로 OVB의 효과이다. 
        - 이 책에서의 예제에서 이 차이는, 소득이 1만 달러 이상 차이나는 것이므로, 크게 영향을 끼침을 알 수 있다. 

## long, short rgression 에서의 공식적인 연결 고리 

> OVB = short regression 에서의 $P_i$의 효과 - long regression 에서의 $P_i$ 의 효과 = $\beta^s - \beta^l = \pi_1 \times \gamma$

-  여기서 $\pi_1$는 아래 공식에서 $P_i$의 계수이다. 

<!-- 3번 수식 -->

$$\begin{align} 
A_i = \pi_0 + \pi_1 P_i + u_i
\end{align}$$

- OVB 를 책의 또다른 수식으로 표현해보자. 

<!-- 4,5번 수식 -->

$$\begin{align} 

lnY_i = \alpha + \beta P_i + \sum^{150}_{j=1} \gamma_j GROUP_{ji} + \delta_1 SAT_i + \delta_2 lnPI_i + e_i \\ 
lnY_i = \alpha^l + \beta^l P_i + \sum^{150}_{j=1} \gamma^l_j GROUP_{ji} + \delta_1^l SAT_i + \delta_2^l lnPI_i + \lambda FS_i + e_i

\end{align}$$

- 4, 5번 수식의 차이는 $\lambda FS_i$ 이다. 이는 교재에서는 가족의 명수이다. 
    - 자녀가 많을수록, 학비 부담이 심해 사립대학교 선택에 영향을 주었을 수도 있다는 내용이다. 

- 이 때의 OVB 는 아래와 같다.

<!-- 6번 수식 -->

$$\begin{align} 
OVB = \beta - \beta^l = \pi_1 \times \lambda
\end{align}$$

- 여기서의 $\pi_1$은 3번 수식과 같은 회귀 모형에서 나왔다고 볼 수 있다. 




