---
title: '[Hexo] Github Page로 블로그 만들기 03'
categories:
  - Web
tags:
  - hexo
  - web
  - blog
  - github
  - develop
date: 2018-02-25 16:57:21
---

## Hexo 시작해보기

앞 선 포스팅에서 밝혔지만 지금 보는 블로그 [icarus 테마](https://github.com/ppoffice/hexo-theme-icarus)가 적용되어있다.

사실 블로그를 만들어야 겠다는 생각은, [Intro 포스팅](https://blinders.github.io/tech_blog/2018/02/18/intro/)을 보면 알겠지만 오래된 생각이다.
그러다 더 이상 미루고 미루다가는 절대 안 할 거 같은 수동적 성격의 나를 채찍질해서 집 근처 스벅으로 오게되었다.
(사실은 설 귀성 기차가 저녁 6시라 이때다 싶었다..)

### Github 작업거리

블로그를 만들기 위해서는 무엇보다도 
**첫 번째, 블로그를 서비스할 Github repository를 생성**해야 한다.
내 경우에는 tech_blog라는 이름의 repository를 생성하고 
Settings 에서 Github Page 를 master 브랜치로 설정 후 Save 해줬다. 
(굳이 master 브랜치가 아니라 다른 브랜치로 해도 상관은 없다.
다만 일부 repository의 경우 로컬에서 master 브랜치로 Direct Push가 안 되는 경우도 있으니 
이 경우엔 Github Page 서비스 브랜치를 다른 걸로 바꾸거나
다른 브랜치에 Push해서 Pull Request를 날리도록 하자.)

### 로컬 작업거리

상세한 포스팅을 보기 전에, hexo로 블로그를 띄우는 명령어만 순서대로 뽑아보면 아래와 같다.
```
npm install hexo-cli -g
hexo init tech_blog
npm intall
hexo server

```
**겨우 4줄!** 
겨우 4줄만 터미널에 입력해주면 나만의 블로그가 생성되는 것이다.

자, 이제 일련의 과정을 좀 상세히 풀어보겠다.
Github의 준비는 끝났으니 이제는 로컬에서 필요한 작업을 해 줄 차례다.

사실 hexo는 예전에 회사에서 사내 Github 도입기념으로 사내 블로그나 만들어볼까 싶어 건드린 적이 있었다.
(이라고 하기엔 벌써 몇 달 전이니 그게…사실 써봤던 녀석이라 'Jekyll vs Hexo'에서 선택된 이유 중 하나다.)

앞 선 포스팅에서도 말했듯이 hexo는 npm을 이용해서 설치를 해준다.
그렇기에 Node.js가 설치되어 있지 않다면 [이 링크](https://nodejs.org/en/download/)를 통해 설치해주길 바란다.

Node.js가 설치 완료되었다면 hexo로 블로그 관련 파일들을 생성할 디렉토리로 이동한 뒤
터미널(window는 cmd나 powershell)을 열어준다.

npm을 통해 hexo를 설치해주기 위한 명령어는 아래와 같다.
```
npm install hexo-cli -g
```
위 명령어로 hexo 를 global(어디서 터미널을 열든 hexo 명령어를 쓰겠다는)로 설치한다.
(..하려 했는데 root 권한이 필요하다. `sudo -s` 로 유저를 root로 변경 설치해주세요)

다음으로 현 위치(블로그 관련 파일들을 받을 디렉토리)에서 
```
hexo init tech_blog
```
를 입력한다.

hexo init 만 입력해도 블로그 관련 파일들이 생성되는데는 문제가 없다.

다만, 뒤에 디렉토리명을 붙이면 동명의 디렉토리가 생성되면서 거기에 파일들이 생성되는 것이다.
hexo init 를 했을 때의 **주의점은 명령어를 실행한 위치에 파일들이 생성되기 때문에 해당 디렉토리에는 그 어떤 파일도 있어서는 안 된다는 것**이다.
만약 단 하나의 텍스트 파일정도만 존재해도 hexo init 명령어는 Error 메시지를 뱉으면서 생성에 실패하게 된다.

hexo init 후 조금만 기다리면 콘솔이 주루루루룩 위로 넘어가더니 뙇하고 각종 파일들이 생성될 것이고
아마 기본적인 디렉토리 구조는 아래와 같을 것이다.

```
tech-blog
├── _config.yml
├── package.json
├── scaffolds
|   ├── draft.md
|   ├── page.md
|   ├── post.md
├── source
|   └── _posts
└── themes

```

생성된 디렉토리로 이동 후 **가장 먼저 해야 할 건 dependency package를 통해서
package.json 에 명시된 package를 설치해주는 것**이다.

```
npm install
```
을 입력해주면 또 콘솔이 주루루루룩 하면서 위로 넘어가더니 뙇하고 끝이 난다.

자,이제 이 것만으로도 블로그 띄울 준비는 85%는 끝난 것이다.
가볍에 콘솔에 아래 명령어를 입력해보자.
```
hexo server
```
그러면 _http://localhost:4000_ 으로 hexo server가 뜨는 것을 확인할 수 있다.
(hexo의 기본 테마는 landscape 로 되있기에 설정의 변경없이 그냥 서버를 띄웠다면 
우주의 까만 배경으로 빛무리가 뜨왛하는 landscape 테마가 보이는 게 정상이다)

hexo를 통해 블로그를 띄웠으니 이젠 설정에 대한 부분을 조금 설명하겠다.

hexo의 모든 설정은 \__config.yml_ 파일 에서 담당한다.
가져다쓰는 테마들은 모두 각 테마들만의 \__config.yml_ 파일을 가지고 있는데
**root 디렉토리에 있는 \__config.yml_ 파일이 총괄대장역할**을 하며
**테마 디렉토리 안에 있는 \__config.yml_ 파일들은 위치에 맞게끔 각 테마들을 담당하는 부대장**이라 할 수 있다.
(그렇기에 root의 \__config.yml_ 내부에 theme 속성 값으로 부대장을 임명하면 해당 테마가 동작하는 방식이다)

root의 \__config.yml_ 에서 타이틀이나 subtitle, description, root url등의
굵직한 설정들-총괄대장이니까-을 추가, 변경, 삭제등 관리할 수 있다.
_(아래에 삽질2라는 이름으로 포스팅을 했는데, 여기서 root url 부분을 간과한게 내 뒷통수를 때렸다)_

이제 로컬에 띄운 블로그를 아~~까 만든 Github Repository에 배포해보려고 한다. 
배포를 하려면 **당연히 배포처를 지정**해야 하고 hexo의 모든 설정은 \__config.yml_ 이 한다고 이야기해왔다.
배포처 설정도 마찬가지로 \__config.yml_ 에 있는데 해당 파일을 열어보면 맨 아래에

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: 
```

요런 상태로 초기 값이 텅 빈 상태일 것이다. 
이제 여기에 위에서 생성한 Github Reposity를 설정해주면 되는데

```
deploy:
  type: git
  repo: https://github.com/GithubUsername/RepoName.git
  branch: master
```

위와 같은 값으로 입력하면 된다.
**type은 git** 이고 **repo는 배포하려는 Github Repository의 URL**이 들어가며
**branch는 배포 시 push 될 타겟 브랜치**를 적으면 된다.

자, 이제 저기까지 설정이 끝난 상태에서
```
hexo generate
```

명령어를 실행하면 _index.html_ 을 포함해서, 
Github Repository에 올라갈 정적 파일들이 _public 디렉토리_ 아래로 생성된다. 

파일들의 생성을 확인했다면 
```
hexo deploy
```
이 명령어로 Github Repository로 hexo가 배포될 것이다.

...그렇게 배포되어야 하는데...무사히 잘 올라가야 되는데...읭?
**Error Deployer not foundgit??** 에러? 읭?

이게 뭐지, 하고 구글링을 해보니 **배포 대상이 Github일 경우 npm으로 설치해줘야 할 패키지가 또 있었다**
(아니, 이런 건 기본으로 좀 넣으라고 hexo님들아..)

그래서
```
npm install hexo-deployer-git --save
```
명령어를 통해 배포를 위한 전용 npm package를 추가 설치해줘야 한다.
(npm의 --save 옵션에 대한 건 하단에 별첨을 참고바란다)

자, 배포에 필요한 패키지도 설치했으니 다시 
```
hexo deploy
```
명령어를 실행해주면 깔끔하게 지정해 준 Github Repository로 배포되는 것을 확인할 수 있다.

그러고나서 Github Repository에 접속해서 지정된 URL로 들어가면 쫘잔, 하고 로컬에서 띄웠던 페이지가 나온다.
(Github Page의 경우 배포 후 즉각 반영되진 않는다. 물론 수분내로 반영되지만 딜레이가 좀 있음을 알아두자)

자, 그럼 이제 직접 만들고 배포한 Github Page가 _이상없이 동작하는 것을_ 확인할 수 있을 것이다.

...정말? 잘 나오나요? CSS 하나도 안 깨지고, resource들 잘 읽어옵니꽈??
**그럼 요 아래는 안 읽으셔도 됩니다.  네? 깨져요? 그럼 요 아래 좀 더 읽으세요.**
(참고로 전 깨져서 여기서 한동안 삽질을 했습니다. 하...ㅠㅠ)

### 몇가지 삽질

**삽질 1.**
몇 번이나 언급했지만 hexo는 로컬에서 **정적파일로 떨어트린 뒤**에 Github에 업로드한다.
 
정적파일로 떨어트리는 이 과정(`hexo generage`)에서, 
기존 로컬에 남아있던 찌꺼기들로 인해 새로운 정적파일이 만들어질 때 불순물이 섞일 수도 있다고 한다.
(어떤 파일, 데이터, 뭐가 불순물인지는 명확히 모르겠습니다. 그걸 알면 내가 이미 Guru지…)

그래서 `hexo generate`를 하기 전에 `hexo clean` 을 실행해서 청소를 한 번 싹 해줍니다.
이러면 `hexo clean` 하는 과정에서 뭔가 delete 되었다는 걸 확인할 수 있습니다.
그 후에 `hexo deploy`를 통해 Github으로 배포해보시기 바랍니다.
(참고로 `hexo deploy —generate` 를 하면 정적파일을 로컬에 떨군 뒤에 **배포까지 한 방**에 해버립니다)

명령어만 순차적으로 나열해서 요약하자면 아래와 같군요.
```
hexo clean
hexo deploy -generate

```

이제 되나요? 되면 그만 읽으셔도 되구요.
여전히 안 되나요? 그럼 좀 더 읽어주세요ㅋㅋㅋㅋ

**삽질 2.** 

이게 제가 삽질한 문제점입니다
(삽질1은 그냥 이 삽질을 해결코자 구글링을 하다보니 찾은 문제라, 이런 경우도 있구나 한 거구요)

저는 애초에 Gitub을 통해서 여러개의 블로그를 운영할 계획이었습니다.
메인 블로그(개인 프로필과 서브 블로그들의 링크만 담당)가 있고 
기술 블로그, 글, 사진 블로그등을 생성할 생각이기 때문에 
일부러 Repository의 이름에도 tech라는 단어를 넣어서 tech_blog로 한 것인데요.

**여기서 문제가 발생**한 겁니다.

커스터마이징이 가능한 대부분의 서비스(앱이든 홈페이지든 뭐가 됐든)는 
최소한의 기능만을 디폴트로 제공하고 너님이 필요하시면 수정해서 쓰세요, 라는 것이 정석입니다. 
hexo도 당연히 그런 불문율을 따르고 있구요. Github 또한 그렇습니다.

**그 중에 하나가 바로 Github Page의 URL 규칙**인데요.
기본적으로 **Github은 username을 바탕으로 Page의 URL을 제공**합니다.
제 Username인 blinders를 예로 들자면 https://blinders.github.io/ 의 형태가 디폴트입니다. 
즉, https://username.github.io/ 의 형태이지요. 
(이에 대한 건 [[Hexo] Github Page로 블로그 만들기 01](https://blinders.github.io/tech_blog/2018/02/21/Hexo-blog-make-01/)의 아래 별첨에도 포스팅했습니다)

그럼 여기서 내가 별도로 생성한 Repository에 블로그를 생성한다면?
네, **URL의 기본형태는 https://username.github.io/RepoName**가 됩니다.
그리고 Github에서 저 URL을 root로 잡아버리기 때문에, 
정적인 파일로 떨궈서 서비스하는 hexo의 경우에는 
필요한 resource들의 경로를 제대로 잡지 못 하는 문제가 발생합니다.
(아,내가 이것 때문에 얼마나 허망한 구글링의 시간을 보냈던가ㅠㅠ)

이건 어떻게 해결해야 할까요? 
당연하게도 Github Page에서 명명한 URL 규칙을 우리가 바꿀 수는 없으니
hexo의 설정을 건드려줘야 합니다. 네, root 디렉토리의 \__config.yml_ 에 해당 설정관련 값이 있습니다.

\__config.yml_ 을 열어보면 상단에

```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://yoursite.com
root: /
```

이런 게 있습니다.
…**네, 떡하니 써있네요.**
너님의 사이트가 서브디렉토리를 쓰면 root 설정에 값을 추가해주라고...
무심결에 제대로 읽어보지 않고 성급히 구글링부터 한 제 잘못이네요..크읗ㅠ

이제 해결해 봅시다. 저기 root 항목에 `/RepoName/` 을 적어주고
```
hexo clean 
hexo deploy —generate
```
를 해줍니다. 그럼 주루루룩 뜨더니 슝 하고 파일들이 Github Repository에 안착할 텐데요.
이제 블로그 URL로 들어가보시면 CSS도 깨지지 않는 평안한 블로그를 보실 수 있을 겁니다.

아, 험난한 블로그 생성기네요. 지나고 나니 별 거 아닌데 넘나 힘든 것..
마침 에픽하이 노래, 빈차가 나오는데 가사가 마음에 와닿네요.
_자라지 않으면 성장통도 그저 pain_
크으, 에픽하이 가사는 정말 사골국물이에요, 
울궈먹고 울궈먹어도 새롭고 이성보단 감성에 꽂혀주시네요ㅠㅠ

...네, 샛길로 새는 걸 보면 아시겠지만 이 글은 여기까집니다.

다음엔 실제 포스팅을 해보고 포스팅 하는 거랑…
..아, 그 전에 일단 css랑 메뉴(카테고리나 아카이브나 프로필이나)들부터 
좀 더 제 입맛에 맞게 커스터마이징하고 후기를 써야 겠군요. 
그럼 다음편에 뵐게요.

 
------------
1. *npm install hexo-deployer-git --save* : --save 옵션은 **package.json을 함께 업데이트** 해 줍니다. 
나중에 이런 귀차니즘이 또 발생하지 않도록… --save에 추가로 --save-dev 라는 옵션도 있는데 
둘의 차이는 package.json 내부에 업데이트를 해줄 때, 
대상으로 쓰여질 json 객체가 dependencies 냐 devDependencies냐의 차이입니다.
2. dependencies 와 devDependencies의 차이는 npm install 할 때 발생하는데.
npm install은 기본적으로 package.json에 명시된 객체값들을 바탕으로 
의존(dependency) package들을 설치해줍니다. 
이때에 **dependencies의 값은 항상 설치**되고 
**devDepenencies의 값은 --production 옵션을 붙이면 빠지게 됩니다.**.
production에선 개발급(devDepenencies)은 뺀다는 의미로 받아들이시면 될 거 같습니다.
만약 npm install “$package” 명령어를 통해서 하나하나 설치하신다면
--dev 옵션을 붙이셔야 devDepenencies의 패키지들이 설치가 됩니다.