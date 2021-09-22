---
title:  "SQL을 이용한 리텐션(retention) 구하기"
excerpt: "리텐션의 개념 및 쿼리를 이용한 리텐션 구하기"

categories:
  - SQL

toc: true
toc_sticky: true

use_math : true
comments : true
image : true
sitemap :
changefreq : daily
date: 2021-07-10
last_modified_at: 2021-07-17
---

## 들어가기 전에

최근 리텐션과 관련된 자료를 만들 일이 있어 공부한 내용을 정리해본다. 공부를 위해 구글링을 하다가 앰플리튜드의 블로그 글을 읽게 되었는데, 리텐션을 정리한 글 중에는 최고봉 인 것 같아 개념에 대한 내용을 굳이 내가 중복해서 적을 필요는 없을 것 같다. 정확히는 앰플리튜드를 국내에 공급하는 ab180이라는 회사가 앰플리튜드의 글을 번역한 것이라 할 수 있겠다.


<p align="center"><img src="/assets/img/retention/ab180_blog_1.png"></p>
<center>(이미지 출처 : https://blog.ab180.co/category/amplitude)</center>  

<!-- ![image](/assets/img/retention/ab180_blog_1.png)
url : https://blog.ab180.co/category/amplitude -->

링크에 블로그 목차를 걸어두었는데, 리텐션과 관련된 대부분의 내용이 해당 블로그에 있으므로, 자세한 설명은 저 글을 참고하자.

또한, 마이리얼트립의 양승화 님이 쓰신 책을 아주 감명 깊게 읽었으니, 이 책을 읽는 것도 매우 좋은 방법인 것 같다.([링크](http://www.yes24.com/Product/Goods/64094963))

## 리텐션이란?

더 잘 작성되어진 블로그 안내 링크를 달았지만, 이 글의 중심 주제인 sql로 리텐션 구하기를 하려면, 우선 간략하게나마 리텐션에 대한 설명이 필요할 것 같다. 앰플리튜드의 글을 보고 내가 이해한 리텐션은 아래와 같다.

1. 리텐션이 왕이다(Rentention is king)
- SaaS에서 중요하다고 하는 kpi는 dau, mau 부터 해서 여러가지가 있겠지만 결국 리텐션이 가장 중요하다는 이야기 이다. 일반적으로 신규 유저 유입 비용 > 기존 유저 유지 비용으로 알려져 있기도 한데... 뭐, 그냥 다 떠나서 상식적으로 생각해보자. 매일 50명의 사람들이 들어오는데, 들어온 사람들이 얼마 안 있다가 우리 서비스를 쳐다보지도 않는다면, 50명의 사람들을 유입 시키는데 비용만 그냥 매일 나가는 것이다. 붙잡아 두는 것이 중요하고, 결국 '잔존'시키는 문제로 넘어가면서 잔존율, 리텐션이 중요한 것이다.

2. 리텐션은 일반적으로 '접속'을 기준으로 보지만, 다른 이벤트를 기준으로 할 수도 있다.
- 몇 번 봤던 스타트업의 투자 관련 기사나 신규 서비스 런칭 후 성과를 측정하는 뉴스에서 언급된 리텐션은 대체로 접속을 기준으로 한 리텐션들이었다. 페이스북의 리텐션은 40%라든가, 혹은 이번에 새로이 출시 된 모바일 게임의 리텐션 등에 대해 얘기할 때는 주로 접속과 관련된 리텐션을 본다. 하지만, 모든 리텐션의 기준이 접속을 하냐 마느냐로만 따지는 것은 아니다.
- 서비스에서 중요하게 생각하는 핵심 이벤트가 무엇이고, 해당 서비스의 특징에 따라 다를 수 있는데, 페이스북이나 모바일 게임 같은 소셜 서비스, 혹은 게임 같은 경우에는 유저들이 매일 접속하는 것이 중요하고, 이게 곧 매출과 연결이 되기 때문에 이러한 수치들을 중요 시 여기는 것이다.
  에어 비앤비와 같은 여행 관련 서비스를 제공하는 기업이라면, 유저가 매일 들어오도록 할 필요가 없을 것이고, 오히려 여행을 많이 준비하는 성수기 같은 기간 등에 접속은 많이 하지 않더라도 예약하는 것이 중요할 것이다.
- 때문에 리텐션을 보고자 할 때는 2가지를 정해야 하는데, 첫 번째는 핵심 이벤트를 정의하는 것이고, 두 번째는 유저들이 우리 서비스를 사용하는 주기를 파악하는 것이다.
핵심 이벤트는, 위에서 언급되었다 시피, 접속이 될 수 도 있고, 일반적으로는 구매나 과금이 중요하니 구매나 과금을 하는 것을 핵심 이벤트로 정의할 수 있다. 리텐션을 높이기 위해서는 결국 유저가 서비스를 계속 써야하기 때문에, 핵심 이벤트는 서비스가 유저에게 제공하고자 하는 가치와 맞닿아 있는 것으로 설정하는 것이 중요하다. 그래야 유저가 서비스의 진정한 가치를 깨닫고, 지속적으로 사용할 것이기 때문이다.(물론 유저가 실제로 원하는 제품이 아닌, 내가 필요하다고 생각해서 만든 제품이라면 계속 사용하지 않을 것이다. 이 부분은 Product-Market Fit 개념과 맞닿아 있다. )

3. 서비스의 특징 또는 산업의 특징에 따라 사용할 수 있는 리텐션의 종류는 다양하다.
- N-Day Retention : 클래식 리텐션이라고도 하는데, 일반적으로 핵심 이벤트를 접속으로 정의하고 1일, 7일, 30일 리텐션을 많이 보는 것 같다. 최초로 서비스에 가입하거나, 서비스에 유입 된 시점을 기준으로 해당 유저들이 7일 차에는 접속을 하는지, 30일차에는 접속을 하는지 파악하는 것이고, 당연히 7일차와 30일차의 리텐션을 확인했을 때 많은 사람들이 남아 있는 것이 좋을 것이다.
N-Day retention의 단점은 특정일에 핵심 이벤트를 발생시키지 않으면, 리텐션 계산 시 제외 된다는 것이다. 서비스에 유입된 유저가 6일차까지 서비스를 이용하다가, 7일 차에 바빠서 들어오지 못해도, 이 유저는 7일차 리텐션에서 제외된다. 하지만, 이 유저는 충분히 서비스를 지속적으로 사용하고 있다고 볼 수 있으므로, 이러한 부분을 놓치게 된다. 그 외 장점으로는 딱 들었을 때 직관적으로 이해하기 좋다는 것이다.
7일 차 리텐션은 가입 후 또는 첫 접속 후 7일 차에 얼마나 들어왔는지 알 수 있다.
- Range Retention : 직역하면 범위 리텐션인데, N-Day retention의 단점이었던 엄밀하게 측정하는 부분을 조금 완화시킨 것이라는 생각이 들었다. 일 자 별로 정확하게 카운트하던 N-Day retention 과 달리, 1주일, 1달, 또는 3달 등으로 범위를 정해주는 것이다. 어떤 범위가 적정한지는 분석을 통해 파악해야 겠지만, 이 역시도 서비스의 특징에 따라 다르다. 봐왔던 자료에서는 배달 앱은 1주일, 여행 서비스는 6개월 뭐 이렇다는데 얼핏 들어서는 타당해 보이기는 한다.
- Rolling Retention : 위의 리텐션과 조금 관점이 다른 특이하다면, 특이하다고 할 수 있는 리텐션이다. 위의 리텐션은 "유저가 서비스를 계속해서 쓰고 있나?" 라면 rolling retenton 의 관점은 "유저가 서비스를 더이상 쓰고 있지 않나..?" 이다.  
  예를 들어보자. 서비스를 런칭하고 30일 차가 되었다. 리텐션을 구해보니, N-day retention에서 N을 7로 놓으면, 7일차 리텐션인데, 7일 차 리텐션이 10%라는 것은 처음 서비스를 쓴 유저 10명의 유저 중 1명의 유저만이 7일 뒤에도 썼다는 것이다. 비록 7일차에는 1명만 쓰긴 했지만, 8일 차, 10일, 15일차에도 유저들이 쓸 수도 있다. 물론 안 쓸 수도 있다.
 반면, rolling retention이 7일차에 10%라는 것은, 처음 서비스를 쓴 유저 10명 중에 1명 빼고, 나머지 9명은 7일 뒤부터 rolling retention 수치를 구하는 이 시점까지 한 번도 서비스를 쓰지 않았다는 것이다.  

## sql로 n-day 리텐션 구하기(presto sql 기준)

** 급하게 정리하는 것이므로 틀릴 수 있음. 대충 개념만 정리 **  

우선은 코호트 분석을 추가하지 않은 상황으로 구해보자.
대부분이 접속을 기준으로 리텐션을 구하니, 핵심 이벤트를 접속이라고 하고 아래와 같은 형태의 테이블을 가정하고, 테이블 이름은 session이라고 하자.   
아래 테이블의 의미는 21년 1월 1일에 id가 1인 유저가 방문 했고, 21년 1월 2일에는 id가 1과 2인 유저가 모두 방문한 것이다. joindate라는 컬럼을 만들어서 유저 별로 가입 일자를 만들었다. 대체로 첫 접속 일자와 동일하다고 볼 수 있을 것이다.

| date(timestamp)       | id(integer)  | joindate(timestamp)   |
|------------|-----|------------|
| 2021-01-01 | 1   | 2021-01-01 |
| 2021-01-02 | 2   | 2021-01-02 |
| 2021-01-02 | 1   | 2021-01-01 |
| ...        | ... |            |

{% highlight sql %}
-- n-day retention
SELECT
  DIFF_DAY('DAY', date, joindate) AS n,
  COUNT(DISTINCT(id)) AS UserCount,
  COUNT(DISTINCT(id)) / (SELECT COUNT(DISTINCT(id)) FROM session) AS n_day_retention
FROM session
GROUP BY DIFF_DAY('DAY', date, joindate)
{% endhighlight %}

범위를 1달로 가정하고, range retention을 구하면 아래와 같이 구할 수 있다.

{% highlight sql %}
-- range retention
SELECT
  DIFF_DAY('MONTH', date, joindate) AS n,
  COUNT(DISTINCT(id)) AS UserCount,
  COUNT(DISTINCT(id)) / (SELECT COUNT(DISTINCT(id)) FROM session) AS range_retention
FROM session
GROUP BY DIFF_DAY('MONTH', date, joindate)
{% endhighlight %}

rolling retention을 구하는 것은 조금 다른데, 우선 마지막 접속일을 구해야 하는데, 구했다고 치고, 기존의 session table을 아래와 같이 가정하자

| date(timestamp)       | id(integer)  | joindate(timestamp)   | lastlogin(timestamp)  |
|------------|-----|------------|------------|
| 2021-01-01 | 1   | 2021-01-01 | 2021-01-10 |
| 2021-01-02 | 2   | 2021-01-02 | 2021-01-14 |
| 2021-01-02 | 1   | 2021-01-01 | 2021-01-10 |
| ...        | ... |            |            |

아래와 같은 순서의 쿼리를 통해 rolling retention을 구할 수 있다.

우선, 첫 번째로, 유저마다 회원 가입 시점과 마지막 로그인의 날짜를 뺀 값을 구하고, 이 뺀 값을 기준으로 유저의 수를 센다.

{% highlight sql %}

WITH T1 AS (
  SELECT
    DATE_DIFF('DAY', joindate, lastlogin) as diffday,
    LAG(COUNT(DISTINCT(id)), 1) OVER (ORDER BY diffday) AS lag_cnt
  FROM session
  GROUP BY DATE_DIFF('DAY', joindate, lastlogin)
  )

{% endhighlight %}

그럼 그 결과물로 아래와 같은 테이블을 얻을 것이다.

| diffday | cnt |
|---------|-----|
| 0       | 100 |
| 1       | 30  |
| 2       | 15  |
| 3       | 5   |
| ...     | ... |

이 테이블의 의미는, 회원 가입 첫 날에 100명의 유저가 가입했다고 가정하면, 회원 가입 이후 1일,2일 차에 각각 접속하고, 더 이상 접속하지 않은 사람이 30명, 15명이라는 의미이다. 즉, 2일 차의 잔존 유저수는 100명(전체 가입자 수) - 30명(1일차가 마지막 로그인이므로 2일차 기준에서는 나간 사람들) = 70명이고, 잔존율은 70명/100명 이므로 70%이다. 쿼리 상에서는 누적 합을 이용하였다.

{% highlight sql %}

SELECT
  diffday,
  ((SELECT COUNT(DISTINCT(id)) FROM session) - cumsum) / CAST(SELECT COUNT(DISTINCT(id)) FROM session AS DOUBLE) * 100e0 AS rolling_retention
FROM
  (SELECT
    diffday,
    cnt,
    SUM(lag_cnt) OVER (ORDER BY diffday ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS cum_sum
  FROM T1) as t2

{% endhighlight %}

- 중간에 누적합을 구하기 위해 window function을 사용했고, window frame을 지정해주었는데, presto sql에서는 window function의 default window frame으로 RANGE UNBOUNDED PRECEDING AND CURRNET ROW 이 설정 되어있다. 따라서,현재 구하고자 하는 누적합의 개념과 동일해서, 따로 적지 않아도 되었지만, window function이 익숙하지 않은 입장에서 상기시키고자 굳이 한 번 적었다.  

## 코호트로 쪼개서 range retention 구하기
리텐션은 대부분의 경우, 위 쿼리와 같이 단일 수치로 계산하기 보다는 코호트 분석을 함께하여 가입 시점이나 첫 구매 등의 특정 행동을 함께한 유저들을 기준으로 하나의 그룹으로 묶어서 본다. 코호트와 관련된 자세한 설명은 역시나 훨씬 더 잘 정리해주신 분의 링크를 첨부한다.([링크](https://entrench-consulting.com/ko/analytics-consulting/%ec%bd%94%ed%98%b8%ed%8a%b8-%eb%b6%84%ec%84%9d%ec%9d%84-%eb%b9%84%ec%a6%88%eb%8b%88%ec%8a%a4%ec%97%90-%ed%99%9c%ec%9a%a9%ed%95%98%eb%8a%94-%eb%b2%95/#page-content))

기존에 사용하던 session이라는 테이블과 핵심 이벤트를 접속으로 그대로 정의한 채로 구해보자. 코호트의 기준은 가입 시점이다.
먼저, 결과적으로 만들고 싶은 형태의 테이블은 아래와 같다.

| joindate | diffday | user_count | total_count |
|----------|---------|------------|-------------|
| 2021-01  | 0       | 1000       | 1000        |
| 2021-01  | 1       | 600        | 1000        |
| 2021-01  | 2       | 300        | 1000        |
| ...      | ...     | ...        | ...         |
| 2021-02  | 0       | 700        | 700         |
| 2021-02  | 1       | 500        | 700         |
| ...      | ...     | ...        | ...         |

- joindate : 유저 별로 가입한 시점을 연, 월 기준으로 잘라냈다.
- total_count : 21년 1월에 가입한 유저의 수이다.
- diffday : 가입 시점을 기준으로 몇 개월이 지났는지이다.
- user_count : diffday와 매핑되는 유저의 수이다. 즉, 가입 후 n개월이 지난 후 유저의 방문자 수 이다.
- 해석에 주의할 점은, 예를 들어 21년 1월 기준으로 diffday가 1이고, 유저 수가 600명이라는 의미는, 21년 1월 가입자 1000명 중에 2월에 방문한 유저가 600명이라는 의미는 아니다. 현재 diffday는 시간과 시간의 차이를 이야기하고 있으므로, 1월 31일에 가입해서 2월 1일에 재방문한 유저는 diffday가 0인 행의 유저 수로 카운트 된다.

위 결과물을 얻기 위해 작성한 쿼리는 아래와 같다.

{% highlight sql %}

SELECT
  t1.joindate,
  t1.diffday,
  t1.user_count,
  t2.total_count
FROM
  (SELECT
    DATE_FORMAT(joindate, '%Y-%m-%d') AS joindate,
    DATE_DIFF('MONTH', joindate, date) AS diffday
    COUNT(DISTINCT(id)) AS user_count
  FROM session
  GROUP BY 1, 2) AS t1
INNER JOIN
  (SELECT
    DATE_FORMAT(joindate, '%Y-%m-%d')) AS joindate,
    COUNT(DISTINCT(id)) AS total_count
  FROM session
  GROUP BY 1) AS t2
  )
ON t1.joindate = t2.joindate
ORDER BY t1.joindate, t1.diffday
{% endhighlight %}

## 마치며..

코호트 분석을 추가해서 리텐션을 볼 경우의 장점은, 예를 들어서, 21년 1월에 가입한 사람들이 21년 2월에 가입한 사람들보다 리텐션이 낮은지 좋은지 알 수 있고, 이로 인해 더 좋은 인사이트를 얻을 수 있다.

몇 주를 벼려서 정리한 리텐션 내용이지만 생각보다 용두사미로 끝난 것 같다. 틀린 내용도 있을 것 같고...두고두고 정리해야겠다..
