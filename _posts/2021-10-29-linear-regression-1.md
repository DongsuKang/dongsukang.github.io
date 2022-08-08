---
title:  "단순 회귀 분석의 개념과 최소 제곱법을 이용한 계수 추정"
excerpt: "단순 회귀분석의 기본적인 개념과 최소 제곱법을 이용해 계수를 추정하는 과정에 대한 내용 정리"

categories:
  - Statistics
  - Regression

toc: true
toc_sticky: true

use_math : true
comments : true
image : true
sitemap :
changefreq : daily
date: 2021-10-29
last_modified_at: 2022-06-19
---


\- 아래 내용은 부산대학교 김충락 교수님의 13년 강의를 KOCW에서 보고 정리한 내용입니다.

(강의 링크 : www.kocw.net/home/search/kemView.do?kemId=703282&ar=link\_gil)

\- 공부 내용을 정리하기 위해 작성하며, 글 중간 중간 제가 개인적으로 추가 내용을 작성한 것이 있는데 당연히 잘못 되었을 가능성이 있습니다. 틀린 부분이 보이시면, 말씀해주시면 감사하겠습니다.

## 회귀 분석 모델의 기본 컨셉
회귀 분석과 관련된 접해볼 수 있는 강의 중 많은 강의가 단순 선형 회귀 분석, 즉, 변수가 하나인 경우의 회귀분석을 우선적으로 다룬다. 다변수보다 개념적으로 이해하기가 쉬우니, 단변수 인 경우에 대해 얘기를 하고, 이를 발판 삼아 확장하여 다변수에 대한 얘기를 하고 싶어 하는 것이다.

우선 기본적으로 회귀 분석의 컨셉은 아래와 같은 함수 f를 만드는 것이다.

$$Y = f(X_1, X_2, \cdots, X_p) + \epsilon$$

여기서 $X_1, X_2, \cdots, X_p$는 개수가 p개인 변수를 의미한다. 회귀분석을 실무에 적용하기 위해 배우는 입장에서 생각을 해보면 종속 변수 Y를 주요 관심사인 매출로 볼 때, X는 매출과 관련될 것으로 기대되는 변수들(방문자수 등)이 있다.

$\epsilon$은 error term, 즉 오차항을 의미하는데, $\epsilon$이 0인 경우, 이를 __결정론적 모델(deterministic model)__ 이라한다. 인풋과 아웃풋의 관계가 명확한 경우로 볼 수 있다.

반면, $\epsilon$ 이 0이 아닌 경우를 regression model이라 하는데, 읽다보면 예상할 수 있지만, 대부분의 경우는 오차항이 0이 아닌 경우일 것이다.

## 회귀 분석 모델의 종류

1. 함수 f의 형태가 알려져 있는 경우를 parametric regression이라 한다.
2. 함수 f의 형태가 알려져 있지 않는 경우(unknown)를 non-parametric regression이라 한다.

위 2가지 모델에 대해서는 자세히 아는 바가 없어 부연 설명은 패스..

## 단순 선형 회귀 분석(Simple Linear Regression)

독립변수가 1개인 단순 선형 회귀 분석에서의 모델은 아래와 같은 형태를 한다.

$$Y_i = \beta_0 + \beta_1 X_i + \epsilon_i, i = 1, \ldots, n $$

여기서 $Y_i, X_i, \epsilon_i$는 각각 i 번째 아웃풋, 인풋, 오차항을 의미한다.
또한 $\beta_0$ 은 절편항(intercept), $\beta_1$은 기울기(slope)라고 한다.

X와 Y에 대한 가정은 아래와 같다.

1. 독립변수 X는 확률 변수가 아닌 **상수**이다.
2. 종속변수 Y는 상수가 아닌 **확률 변수**이다.

X와 Y가 확률변수인지 상수인지는 굉장히 중요하다. 사실 회귀분석을 예전에 배웠음에도 불구하고 무언가 모르고 있다는 느낌을 계속 받았는데, 공부를 하고 있는 현재, 위 2가지 가정을 놓친 것이 뒷 부분을 잘 이해할 수 없게 만들었던 요소 중 하나가 아닐까 한다. 중요한 이유는 이후에 설명한다.

오차항에 대한 가정은 아래와 같다.

$$E[\epsilon_i] = 0, Var[\epsilon_i] = \sigma^2$$

즉, 오차항의 평균은 0이라고 가정하고, 오차항의 분산은 $\sigma^2$ 이라고 가정한다.

## 종속 변수 Y의 기댓값과 분산

Y는 아까 확률 변수라고 했는데, Y가 확률 변수라면, 우리는 Y의 기댓값과 분산을 구할 수 있다.(반면, 상수인 X는 이미 정해져있는 수이기 때문에 기댓값과 분산 또한 상수로 이미 안다고 볼 수 있다.)

$$ \begin{aligned}  
  E[Y_i] &= E[\beta_0 + \beta_1x_i + \epsilon_i] \\
   &= \beta_0 + \beta_1 E[X_i] + E[\epsilon_i]   \\
   &= \beta_0 + \beta_1 X_i \ (\because E[\epsilon_i] = 0) \\
  \end{aligned} $$

따라서 $E[Y_i]$ 의 기댓값은 $\beta_0 + \beta_1 X_i$ 이다.

$$ \begin{aligned}  
  Var[Y_i] &= Var[\beta_0 + \beta_1 X_i + \epsilon_i] \\
   &= Var[\epsilon_i] (\because X_i, \beta_0, \beta_1 \ constant)   \\
   &= \sigma^2  \\
  \end{aligned} $$

## 회귀 계수에 대한 추정(Estimation Regression Coefficients)
표본을 이용해 모수를 추정할 때 사용하는 방법으로 잘 알려진 방법은 크게 2가지가 있다. 최소제곱법(Lease Squares Estimation)과 최대우도추정법(Maximum Likelihood Estimation)이다.

우선, 최소제곱법을 이용해 회귀 모델의 계수를 계산해보자. 회귀 모델의 최소제곱법을 적용할 경우, 아래와 같은 Q를 **최소화**하는 해를 찾는 문제가 된다.

$$Q = \Sigma_{i=1} ^n (Y_i - (\beta_0 + \beta_1 X_i))^2 = \Sigma_{i=1}^n \epsilon_i^2$$

Q를 최소화하는 문제를 찾기 위해, 최소제곱법을 이용할 때, 대수적인 방법과 해석학적인 방법 2가지를이용한다.(다크 프로그래머님의 글 참고 : '최소자승법 이해와 다양한 활용 예'(https://darkpgmr.tistory.com/56)

강의에서는 (다크프로그래머님의 블로그의 표현에 의하면)해석학적인 방법을 선택했다.

$$ \begin{align}  
\frac{\partial Q}{\partial \beta_0} & = -2\Sigma_{i=1}^n(Y_i - \beta_0 - \beta_1 X_i) = 0 \\
\frac{\partial Q}{\partial \beta_1} & = -2\Sigma_{i=1}^n X_i(Y_i - \beta_0 - \beta_1 X_i) = 0
  \end{align} $$

식 (1) 은 회귀 모델 중 절편항에 해당하는 $\beta_0$에 대한 편미분을 진행해주기 때문에, 절편항을 제외한 모든 확률 변수를 상수로 본다. 식(2) 는 기울기($\beta_1$)에 대한 편미분을 하기 때문에, 기울기를 제외한 다른 모든 변수를 상수로 본다. 미분했을 때, 0이 되도록 하는 이유는, 방정식에서 최소, 최대를 찾기 위해 미분한 후 0이 되는 지점을 찾았던 것을 기억하면 된다. 그리고 여기서 해가 되는 $\beta_0$와 $\beta_1$을 각각 $\hat{\beta_0}$, $\hat{\beta_1}$ 이라고 한다.

편미분을 진행한 이후에는 아래와 같은 정규 방정식(normal equation) 형태가 된다.

$$ \begin{aligned}  
\Sigma Y_i & = n \hat{\beta_0} + \hat{\beta_1} \Sigma X_i \\
\Sigma X_iY_i & = \hat{\beta_0} \Sigma X_i + \hat{\beta_1} \Sigma X_{i}^2 \\
  \end{aligned} $$

이를 얻고자 하는 해인 $\hat{\beta_0}$와 $\hat{\beta_1}$로 정리하면 아래와 같다.

$$\hat{\beta_0} = \frac{1}{n}{\Sigma Y_i - \hat{\beta_1}\Sigma X_i} = \bar{Y} - \hat{\beta_1}\bar{X}$$

$\Sigma X_i Y_i$ 는 아래와 같이 정리 할 수 있다.

$$\begin{aligned}
\Sigma X_i Y_i & = (\bar{Y} - \hat{\beta_1}\bar{X})n\bar{X} + \hat{\beta_1}\Sigma X_i^2 \\
& = (\Sigma X_i^2 - n \bar{X}^2) \hat{\beta_1} + n\bar{X}\bar{Y}
\end{aligned}$$

$$\hat{\beta_1} = \frac{\Sigma X_iY_i - n\bar{X}\bar{Y}}{\Sigma X^2 - n\bar{X}^2} =
\frac{\Sigma(X_i - \bar{X})(Y_i - \bar{Y})}{\Sigma(X_i - \bar{X})^2} = \frac{S_{XY}}{S_{XX}}
$$

따라서, 최소제곱법을 이용해 절편항과 기울기를 구하면 아래와 같다.

$$\begin{align}
\hat{\beta_0} & = \bar{Y} - \hat{\beta_1}\bar{X} \\
\hat{\beta_1} & = \frac{S_{XY}}{S_{XX}}
\end{align}$$

우선 여기까지의 내용을 정리를 한 번 해보자.

1.  단순 선형 회귀 모델에서 궁금해하는 절편항과 기울기항의 모수를 추정하기 위해 최소제곱법을 사용했다. 최소 제곱법은 선형대수적으로 풀어나갈 수 있고, 해석학적으로 풀어나갈 수 있지만, 강의에서는 해석학적인 방법으로 풀어나갔다. 그리고 그 방법은 편미분을 이용한 것이다.

2. 최소 제곱법으로 풀고자 하는 문제는 $Q = \Sigma_{i=1} ^n (Y_i - (\beta_0 + \beta_1 X_i))^2 = \Sigma_{i=1}^n \epsilon_i^2$ 를 최소화 하는 것이다.

3. 1번에서 최소제곱법을 풀기 위해 편미분을 사용했다고 했는데, Q를 최소화 하기 위해 $\beta_0, \beta_1$ 을 기준으로 Q를 편미분 했는데, Q를 최소화 하는 $\beta_0, \beta_1$ 를 각각 $\hat{\beta_0}, \hat{\beta_1}$ 이라고 부르기로 한다.

4. 그리고 그렇게 Q를 가장 작게 만들어주는 $\hat{\beta_0}, \hat{\beta_1}$를 찾고 보니 각각 식 (3), (4)의 값이었다.

5. 즉, 단순 선형 회귀 모델의 오차항을 최소로 만드는 절편항은 종속 변수인 Y의 평균과 $\hat{\beta_1}$와 독립 변수 X의 평균에 의존한다. 그리고 기울기항은 독립변수와 종속변수의 관계라고 볼 수 있는 X와 Y의 공분산(=$S_{XY}$)가 클수록, X의 분산이 작을수록 커진다고 볼 수 있다.
또한 $\hat{\beta_0}, \hat{\beta_1}$ 모두 종속 변수이자 **확률 변수 Y에 의존하고 있으므로, 확률 변수라고 볼 수 있다.**


## 최소제곱법을 이용해 추정한 계수의 기댓값과 분산
### $\hat{\beta_0}, \hat{\beta_1}$ 의 기댓값
$\hat{\beta_0}, \hat{\beta_1}$ 이 각각 확률 변수 Y에 의해 그 값이 바뀔 수 있는 상태인, 즉 확률 변수라고 볼 수 있기 때문에, 이 계수들의 기댓값과 분산에 대해 알아보고자 한다. 확률 변수인 상태에서 우리가 이야기 해볼 수 있는 첫 번째가 바로 기댓값과 분산 이기 때문이다.

$$\hat{\beta_1} = \frac{\Sigma(X_i - \bar{X})(Y_i - \bar{Y})}{S_{XX}} = \frac{\Sigma(X_i - \bar{X})Y_i - \Sigma(X_i - \bar{X})\bar{Y}}{S_{XX}}$$

여기서 $\Sigma(X_i - \bar{X}) = 0$ 인데 그 이유는 아래와 같다.


$$\begin{aligned}
\Sigma(X_i - \bar{X}) & = \Sigma X_i - n{\bar{X}}\\
& = \Sigma X_i - n\cdot \frac{1}{n} \cdot \Sigma X_i (\because \bar{X} = \frac{\Sigma X_i}{n}) \\
& = 0
\end{aligned}$$

따라서 $\hat{\beta_1}$ 는 아래와 같이 정리할 수 있다.

$$\begin{aligned}
\hat{\beta_1} & = \frac{\Sigma(X_i - \bar{X})\cdot Y_i}{S_{XX}} \\   
& = \Sigma W_iY_i, W_i = \frac{X_i - \bar{X}}{S_{XX}}
\end{aligned}$$

그런데 위에서 정리한 $\Sigma W_i$ 에는 아래와 같은 특징이 있다.

$$\begin{align}
\Sigma_{i=1}^n W_i &= \Sigma_{i=1}^n \frac{X_i - \bar{X}}{S_{XX}} = \frac{1}{S_{XX}}\cdot \Sigma(X_i - \bar{X}) = 0   \\   
\Sigma_{i=1}^n W_i^2 &= \Sigma_{i=1}^n(\frac{X_i - \bar{X}}{S_{XX}})^2 = \frac{1}{S_{XX}}\cdot \Sigma(X_i - \bar{X})^2 = \frac{S_{XX}}{(S_{XX})^2} = \frac{1}{S_{XX}}
\end{align}$$

따라서 $\hat{\beta_1}$의 기댓값은 아래와 같다.

$$\begin{aligned}
E[\hat{\beta_1}] & = E(\Sigma_{i=1}^n W_iY_i) = \Sigma_{i=1}^n W_iE[Y_i] = \Sigma_{i=1}^n W_i\cdot (\beta_0 + \beta_1 X_i) \\
& = \beta_0 \Sigma W_i + \beta_1 \Sigma W_iX_i \\
& = \beta_1 (\because \Sigma W_i = 0, \Sigma W_iX_i = 1)
\end{aligned}$$

이 때 $\Sigma W_iX_i = 1$인 이유는 아래와 같다.

$$\begin{align}
\Sigma W_iX_i & = \Sigma_{i=1}^n \frac{X_i - \bar{X}}{S_{XX}} \cdot X_i \\
& = \frac{1}{S_{XX}}\cdot \Sigma_{i=1}^n (X_i - \bar{X})X_i \\
& = \frac{1}{S_{XX}}\Sigma(X_i - \bar{X})(X_i - \bar{X}) \\
& = 1
\end{align}
$$

여기서 중요한 점은 식 (8) 에서 (9) 로 넘어가는 과정인데, 이 부분을 이해하기가 꽤나 어려웠다.
(8)에서 (9)로 넘어갈 수 있는 이유는, 간단히 얘기하면 $\Sigma_{i=1}^n (X_i - \bar{X})\bar{X} = 0$ 이기 때문인데, 이게 0인 이유는 아래와 같다.

$$\begin{aligned}
\Sigma (X_i - \bar{X})\bar{X} & = X_1 \bar{X} - \bar{X}^2 + \cdots + X_n\bar{X} - \bar{X}^2\\
& = n \cdot \bar{X} \cdot \bar{X} - n \cdot \bar{X}^2 \\
& = n \cdot \bar{X}^2 - n\cdot \bar{X}^2 \\
& = 0
\end{aligned}$$

따라서 $\Sigma W_iX_i = 1$ 이고, $\hat{\beta_1}$의 기댓값은 $\beta_1$ 이다.

다음으로 $\hat{beta_0}$의 기댓값에 대해 알아보자.

$$\begin{aligned}
E[\hat{\beta_0}] & = E[\bar{Y} - \hat{\beta_1}\bar{X}] \\
& = E[\bar{Y}] - \bar{X} \cdot E[\hat{\beta_1}]
\end{aligned}$$

여기서, $\bar{Y}$ 는 아래와 같이 정리할 수 있다.

$$\begin{aligned}
\bar{Y} & = \frac{1}{n} \Sigma_{i=1}^n Y_i \\
& = \frac{1}{n}\cdot\Sigma_{i=1}^n(\beta_0 + \beta_1 X_i + \epsilon_i) \\
& = \beta_0 + \beta_1 \bar{X} + \bar{\epsilon}, \bar{\epsilon} = \frac{1}{n}\Sigma\epsilon_i
\end{aligned}$$

따라서 $E[\bar{Y}]$ 는

$$\begin{aligned}
E[\bar{Y}] & = E(\beta_0 + \beta_1 \bar{X} + \bar{\epsilon}) \\
& = \beta_0 + \beta_1 \bar{X} + E[\bar{\epsilon}] \\
& = \beta_0 + \beta_1 \bar{X}  (\because E[\bar{\epsilon}] = 0)
\end{aligned}$$

그리고 이를 이용하면 $E[\hat{\beta_0}] = (\beta_0 + \beta_1 \bar{X}) - \bar{X}\beta_1 = \beta_0$ 이다.

### $\hat{\beta_0}, \hat{\beta_1}$ 의 분산

$Var(\hat{\beta_0}), Var(\hat{\beta_1})$은 각각 아래와 같다.

$$\begin{aligned}
Var[\hat{\beta_1}] & = Var(\Sigma_{i=1}^n W_iY_i) \\
& = \Sigma_{i=1}^n W_i^2Var[Y_i] (\because \epsilon_i's : independent \rightarrow Y_i's : independent) \\
& = \Sigma_{i=1}^n W_i^2 \cdot Var[\beta_0 + \beta_1 X_i + \epsilon_i] \\
& = \sigma^2 \Sigma_{i=1}^n W_i^2 \\
& = \frac{\sigma^2}{S_{XX}}(\because \beta_0, \beta_1Var[\epsilon_i] = \sigma^2)
\end{aligned}$$

$$\begin{aligned}
Var[\hat{\beta_0}] & = Var(\bar{Y} - \hat{\beta_1}\bar{X}) \\
& = Var(\bar{Y}) + \bar{X}^2 \cdot Var(\hat{\beta_1}) - 2Cov(\bar{Y},  \hat{\beta_1}\bar{X}), (\because Var(X+Y) = Var(X) + Var(Y) - 2Cov(X, Y)) \\
& = Var(\bar{Y}) + \bar{X}^2 \cdot Var{\hat{\beta_1}} - 2 \cdot \bar{X} \cdot Cov(\bar{Y}, \hat{\beta_1}) \\
& = \frac{\sigma^2}{n} + \bar{X}^2 \cdot \frac{\sigma^2}{S_{XX}} -  2\bar{X} Cov(\bar{Y}, \hat{\beta_1})
\end{aligned}$$

여기서, $Cov(\bar{Y}, \hat{\beta_1})$을 정리하는 과정에서 조금 복잡하다.

$$\begin{aligned}
Cov(\bar{Y}, \hat{\beta_1}) & = Cov(\frac{1}{n} \Sigma Y_i, \Sigma W_i Y_i) \\
& = Cov(\frac{1}{n} \mathbf{1}^t \mathbf{y}, \mathbf{w^ty})
\end{aligned}$$

이 때, $\mathbf{1, w, y}$ 는 각각 아래와 같다.

$$\begin{aligned}
\mathbf{1} & =  (1, 1, \ldots, 1)^t \\
\mathbf{y} & =  (Y_1, Y_2, \ldots, Y_n)^t \\
\mathbf{w} & =  (W_1, W_2, \ldots, W_n)^t
\end{aligned}$$

따라서 $Cov(\bar{Y}, \hat{\beta_1})$ 는

$$\begin{aligned}
Cov(\bar{Y}, \hat{\beta_1}) = \frac{1}{n}\mathbf{1^t}Cov(\mathbf{y})\mathbf{w} = \frac{1}{n} \sigma^2 I \mathbf{w} = \frac{\sigma^2}{n}\mathbf{1w}(\because \Sigma W_i = 0 ) = 0
\end{aligned}$$

따라서 $Var(\hat{\beta_0}) = \sigma^2 ( \frac{1}{n} + \frac{\bar{X}^2}{S_{XX}})$ 이다.

최종적으로 아래 2가지 식을 얻었다.

$$\begin{align}
E(\hat{\beta_0}) & = \beta_0, Var(\hat{\beta_0}) = \sigma^2 ( \frac{1}{n} + \frac{\bar{X}^2}{S_{XX}}) \\
E(\hat{\beta_1}) & = \beta_1,  Var(\hat{\beta_1}) = \frac{\sigma^2}{S_{XX}}
\end{align}$$

## 최종 요약

- 식 (11)과 (12)를 구하게 된 과정은 아래와 같다.
  - 우리가 선형 회귀 모델에서 궁금했던 것은 오차를 최소화 하기 위해 $\beta_0, \beta_1$는 얼마일까?였다.
  - 그래서 $\beta_0, \beta_1$ 를 구하려고 했더니, 이 2개의 모수가 모두 확률 변수 Y와 연관이 있다는 사실을 알았다.
  - 확률변수라고? 그럼 기댓값과 분산은 얼마일까? 라고 해서 구해보았더니 식 (11), (12)를 얻었다.

- 식 (11)과 (12)를 통해 알 수 있는 것은 무엇일까?
  - $\hat{\beta_0}, \hat{\beta_1}$ 의 기댓값은 결국 $\beta_0, \beta_1$ 이다.
    - 즉, $\beta_0, \beta_1$ 자체가 오차를 최소화 시키는 값이었다.
  - $\hat{\beta_0}, \hat{\beta_1}$ 의 분산에 영향을 주는 요인은 오차항의 분산, X의 평균과 X의 분산이다.
    - X의 분산이 클수록 $\hat{\beta_0}, \hat{\beta_1}$의 분산의 크기가 작아진다.
    - $\hat{\beta_0}, \hat{\beta_1}$의 분산의 크기가 작을 수록 해당 계수가 가치를 발휘할 수 있을 것이므로, X의 분산이 작은 것이 단순 선형 회귀 분석에서의 계수 추정에 유리하다.
