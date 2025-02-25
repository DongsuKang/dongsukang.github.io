---
title:  "전환율(Conversion Rate)을 구할 때의 고민 정리"
excerpt: "전환율은 생각보다 심오했다. "

categories:
  - Growth Hacking

toc: true
toc_sticky: true

use_math : true
comments : true
image : true
sitemap :
changefreq : daily
date: 2021-09-22
last_modified_at: 2021-09-26
---


## 들어가기 전에
전환율은 그로스 해킹이라 불리우는 분야에서는 빠지지 않고 나오는 요소이다.   

이 포스팅이 전환율에 대해 아주 전문적인 글이라고는 할 수 없지만, 대부분의 블로그에서 다루는 것보다 더 실무적이고, 실제로 이 전환율을 구할 때 맞닥뜨릴 수 있는 고민들에 대해 다루었기 때문에 더 현실적이라고 말할 수는 있을 것 같다.

개념만 들어서는 그렇게 어렵지 않은 부분이라고 조금 가볍게 생각했었는데, 실제로 직접 구하려고 하다 보니 이렇게 고려할게 많은 줄은 전혀 몰랐다.

## 전환율이란?
전환율은 이름에서 알 수 있듯이 '어떤 비율'을 의미한다. 어떤 비율이냐하면, 정의하기에 따라 나름이겠지만, 일반적으로 '방문한 사람들 중에 어떤 액션을 한 사람들의 비율'이다.(사람이 아닐 수도 있다는 부분을 뒷 부분에서 언급하겠다.). 따라서 일반적인 전자상거래 서비스를 운영하는 입장에서 전환율이 3%라는 것은 홈페이지로 유입된 100명 중에 3명이 구매를 했다 이렇게 볼 수 있다.

물론, '구매'라는 액션에 초점을 맞추지 않고, 회원 가입 등의 다른 주요 이벤트들을 체크하는 곳에 사용할 수 있다. 그럼 구매 전환율이 아니라 회원가입 전환율이라고 볼 수 있다.

전환율이 중요한 이유는, 서비스에 들어온 사람들 중에 실제로 우리가 원하는 액션을 하는 사람들의 비율을 체크하기 위함이다. 모든 지표들이 그렇지만, 전환율 자체도 시간의 흐름에 따라 체크할 필요가 있고, 떨어졌다면 왜 떨어졌는지, 올라갔다면 어떤 활동의 결과로 올라갔는지 등에 대한 분석이 필요하다.

## 전환율을 구하는 방법
전환율을 구하는 방법은 사실 어려울 것이 없다. 로그 데이터를 확인할 수 있는 데이터 분석가라면, 유저들을 식별할 수 있는 식별자 역할을 하는 컬럼이 DB 내에 존재할 것 이고, 그 값을 이용해 '서비스를 이용한 사람들의 수'를 구한다.
그 다음, 전환 이벤트가 발생한 수, 또는 경우에 따라서 전환 이벤트를 한 사람의 수를 센다.

## 그런데 뭐가 어렵다는 거지?
전환율을 구할 때 정작 어려웠던 것은, '몇 일동안 유입된 사람의 수'를 카운트 해서 분모에 넣을 것인지, 또, '몇 일 동안 전환된 사람의 수'를 분자로 놓고 비율을 구할 것인지가 어렵다. 한 가지 예시를 들어보겠다.

일 별 전환율을 구하기 위해 당일 방문한 사람들의 수와 방문한 사람들 중 전환까지 이루어진 사람들의 수를 sql을 이용해서 구하고, 이를 이용해 전환율을 구하고자 한다. 방문한 사람들 중 전환된 사람들의 수를 이야기하므로 전환율의 정의와 크게 다르지 않으니 이 또한 전환율 이라고 할 수 있다.
하지만, 이미지와 같은 상황을 가정해보자

<p align="center"><img src="/assets/img/conversion-rate-using-sql/img_001.png"></p>

A 유저는 20일, 22일, 24일 3번 방문했고, 그 중 24일 방문 때 전환을 했다.
B 유저는 24일에 방문했지만, 방문한 순간 보자마자 전환을 했다. 전환의 기준을 구매라고 본다면, A 유저는 상대적으로 신중한 스타일의 구매자이고, B 유저는 보자마자 구매를 한 플렉스 스타일이라고 할 수 있을 것이다.
그리고 C 유저는 20일에 방문했지만, 그 이외의 방문 기록은 없다.

이렇게 3명의 유저가 남긴 로그데이터를 기준으로 볼 때, 24일 기준의 전환율은 2/2, 즉, 50% 이다. 24일에 방문한 유저는 2명이고, 이 때 전환된 사람도 2명이기 때문이다.

하지만, 24일 하루의 전환율을 구할 때, 방문자수를 24일 하루만 보는 것이 아니라, 4일을 기준으로 본다면 전환율은 달라지게 된다. C 유저가 20일에 방문했기 때문에, 20일부터 24일까지의 방문자수는 3명으로 늘게 되고, 24일의 전환율은 2/3 = 66%가 된다.

이 부분이 앞서 말했던 '몇 일동안 유입된 사람의 수'이다. 24일의 일 별 전환율이 100%와 66% 두 가지 수치가 나왔는데, 이 수치 중 나는 데이터 분석가로써 어떤 수치를 선택해야할까?
**어떤 수치가 현 상황을 더 잘 나타내는 지표라고 판단할 수 있을까? 어떤 기준이 옳은 것일까? 또 그 수치가 옳다고 말할 수 있는 근거는 무엇일까?**

위와 같은 고민을 하면서 전환율에 대한 구글링을 열심히 해보았지만, 마땅히 원하는 성과를 얻을 수는 없었다. 대부분의 블로그는 전환율이 어떤 뜻이고, 왜 중요한지에 대한 설명을 해줄 뿐 이었다. 이 부분에 대한 정확한 정답은 아니지만, 내 나름대로의 결론은 '전환 주기'를 고려 해야 한다는 것이다.

## 전환율을 구할 때는 '전환 주기'를 고려 해야 한다....할까요..?

이 부분이 고민되는 이유는 결국 **유저마다 서비스를 이용하는 패턴**이 다르기 때문이라고 생각한다. 위의 예시에서, A, B, C 유저와 같이 누구는 여러 번 방문한 끝에 한 번 전환되고, 누군가는 비교적 단기간 내에 전환이 된다면, 이들의 이러한 패턴을 고려하면 되지 않을까 라고 생각했다.

<p align="center"><img src="/assets/img/conversion-rate-using-sql/img_002.png"></p>

유저마다 전환 이벤트가 발생하는 간격을 구하고, 이들의 대푯값을 뽑아서 간격을 정할 수 있지 않을까? 만약 전환 이벤트를 구매라고 보고, 유저들이 대체로 1주일에 한 번씩 구매를 한다면, 1주일 동안의 방문자 수를 전환율의 분모로 삼는 식으로 말이다.

확실한 건 아니지만, 하나의 방안으로 적용해볼 만 한 것 같다.

## 그럼 고민은 끝일까?

고민은 끝나지 않는다. 그냥 다음 업무를 하기 위해서 잠시 미뤄두는 것일 뿐... 전환 주기를 고려해서 전환율을 구하려고 하니 또 아래와 같은 고민이 생겼다.

- vip는 자주 구매(전환)한다.
  - 대부분의 서비스에는 vip들이 존재한다. 서비스를 사용하는 유저들 중에서도 정말 특출나게 그 서비스를 사랑하고, 자주 이용하는 사람들이 존재하는데, 문제는 구매를 기준으로 봤을 때, 이들의 구매주기는 다른 유저에 비해 굉장히 짧다는 것이다. 게다가 vip들의 구매횟수는 당연히 많을테니까, 이들의 짧은 구매 주기는 구매 주기에 큰 영향을 미칠 것이다.  

  - 그럼 유저 등급별로 전환율을 나누어서 구하면 될까? 그렇게 하는 경우를 들어보지는 못했지만, 그것도 방법이 될 수 있을 것 같다.
- 주기를 어느 정도 고려 해야할까?
  - 전환 주기를 분위수로 구해보면 분명 다양할 것이다. 커머스라고 했을 때, vip는 1주일동안에도 여러 번 전환될 수 있고, 극단적으로 서비스를 거의 쓰지 않는 유저들은(물론, 서비스에 따라 다르겠지만), 1달에 1번도 잘 안할 수도 있다. 그럼 1달에 1번 쓰는 유저에 기준을 맞추면, 1달에 1번 쓰는 유저와 vip의 방문을 모두 체크할 수 있지 않을까?

## 마치며..
잘 알고 있고, 언제든지 구할 수 있다고 생각한 전환율이라는 개념에 대해 예전보다 몇 단계 깊은 고민을 하면서 든 생각들을 정리해보았다. 전환율은 ga, amplitude, braze 등 많은 툴에서 기본적으로 제공하고 있는 지표이지만, 서로 다른 기준을 적용할 것으로 생각된다. 이 부분에 대해 공부하고, 차이점을 정리하면, 전환율에 대해 더 알아갈 수 있을 것 같기도 하다.
