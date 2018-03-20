---
title: '[Hexo] Github Page로 블로그 만들기 01'
categories:
  - Web
tags:
  - hexo
  - web
  - blog
  - github
  - develop
date: 2018-02-21 21:53:51
---

## Github Blog?
알 사람은 알겠지만 Github은 Repository를 개설한 뒤 Settings에 있는
GitHub Pages 라는 설정을 통해 웹 페이지를 개설 할 수 있다.

해당 설정은 root 디렉토리의 index.html을 통해서 웹페이지를 제공하는 서비스인데
Github을 이용하는 수많은 개발자들, 스타트업, 혹은 일반기업들도
해당 설정을 통해서 자신만의 포트폴리오를 만들거나 
혹은 Repository에 올린 오픈소스의 소개등의 용도로 사용되고 있다.
(간단한 소개는 README.md를 이용하지만...)

## 그냥 쌩으로 해야 되나?

Github을 통해서 블로그를 개설하기로 한 뒤 가장 고민했던 건 어떤 플랫폼을 사용할 건가, 였다.
Github Page가 뭔지는 모르겠고 **일단 띄워만 보자**, 싶다면 아래와 같은 절차를 거치면 된다.

1. 블로그를 위한 Repository를 만든다.
2. 그리고 root 디렉토리에 index.html 파일을 하나 만든다.
3. 생성한 파일(index.html)에 cdn으로 사용하려는 라이브러리를 땡기고
4. style 태그로 css를 넣고 script로 javascript를 넣는다.
5. body에 원하는 문구를 넣는다.

그러면 웹 페이지가 뜨긴 뜬다.
위의 순서가 무슨 소린지 모르겠다면, 아래 코드를 복사해서 index.html 파일에 넣어보자.
아래 코드처럼만 작성해도 우리는 **Hello Grey!** 라는 문구를 브라우져에서 확인할 수 있다.

```
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
  <head>
    <title>Grey Title</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
  </head>
  <body>
    <div>
       Hello Grey!
    </div>
  </body>
</html>

```

아아, 심플하다. 
매우 많이 심플해서 예전에 APM(Apache+Php+MySQL)으로 하나하나 설정하며
웹 페이지 하나를 겨우겨우 띄웠던 과거의 내가 초라해지기까지 하는 느낌이다.

이처럼 겨우 index.html을 만들어 넣어놓는 것만으로도 Github Page는 **웹 페이지로써의** 동작을 해준다.
(아,물론 Repository의 Settings에서 설정을 해줘야 하지만, 이마저도 *메인 Repository*라면 필요가 없다)

하지만 이처럼 한 파일에 다 떄려박는건 너무 옛날 방식이고, 내가 만들려던 건 엄연히 **블로그**다.

그냥 Hello Grey! 를 보여주고 한 페이지로 땡! 하고 끝나는 사이트가 아니라
블로그로써의 동작을 하는 Github Page를 개설하는 것이 목적이다.

그렇기에 **블로그라면** 
> 1. 당연히 **글을 쓸 수 있는 기능**이 있어야 하고
> 2. 그 **글을 보여주는 기능**
> 3. 그리고 글에 대한 카테고리 기능이나
> 4. 추가적으로 태그에 대한 기능이 있으면 더 좋고 
> 5. 인피니티 스크롤이 아닌 이상 페이징도 되야한다.
> 6. 이 외에 부가적인 기능도 있겠지만 핵심은 포스팅이니까 이와같고
> 7. 그렇게 더해서 쓴 글들을 **이쁘게(이건 중요하다) 보여줘야 한다**.
> 보기에 좋은 떡이 먹기도 좋다고, 이뻐야 한다.

뭔가 되게 많은 것 같지만 심플하게 정리를 해보면 내가 원하는 건 2가지다.

1. 블로그로써의 기능
2. 디자인

위와 같은 블로그로써의 핵심기능을 제공하면서도
내가 만들었지만 내가 만들지 않은 것 같은 이쁨을 뿜뿜할 수 있어야 한다.

물론 저 위에 적은 index.html에 장인의 손길로 한땀한땀 작업해서 만들 수는 있다.
하지만 그건 내 입맛에 딱맞는 자동차 하나 만들자고 자동차 공장을 만드는 꼴이다. 배보다 배꼽이 커지는 짓이랄까.

그렇기에 Github Page 를 통해서 블로그를 만들려는 많은 이들은 아마도 생각했을 것이다. 
이걸 자동화 해주는 플랫폼이 있으면 좋겠다, 라고.
그리고 당연하게도 있었으면 좋겠다, 라고 생각하는 서비스와 기능은 이미 있는 게 이 바닥의 정설이다.

심지어 **그런 애들이 2개**나 있다. 
언뜻보면 지킬박사와 하이드라고 읽을 수도 있는 이 두 녀석의 이름은
**Jekyll**, 그리고 **Hexo**다.

------------
1. *메인 Repository* : Github 에서 ID를 생성하면 기본적으로 Username에 대한 블로그를 제공한다.
다만 이또한 Repository를 별도로 생성해야만 관리가 가능하며 
**생성방법은 Repository의 이름을 username.github.io 로 생성**하면 된다. 
해당 Repository를 만들면 Settings에 Github Page 관련 기능이 자동으로 True 상태이며 
**http://username.github.io/ 과 같은 형태로 URL을 제공**한다. 
다음 포스팅에서도 설명하겠지만 이외에 다른 Repository에서 Github Page를 이용하려 한다면 
Settings에서 별도로 설정을 해줘야 하며 URL의 형식또한 http://username.github.io/ 에 
Repository 가 추가로 붙어서 http://username.github.io/RepositoryName 과 같은 형태를 띈다.