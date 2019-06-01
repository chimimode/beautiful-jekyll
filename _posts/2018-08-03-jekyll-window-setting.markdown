---
layout: post
title:  "윈도우 환경에서 github로 jekyll 블로그 만들기"
date:   2018-08-03 00:56:12 +0900
categories: jekyll
tags: [jekyll]
comments: true
---
윈도우 환경에서 깃허브+지킬로 정적 블로그 생성을 했다. 

초반에 설정에 익숙치 않아서 낭비되는 시간이 너무나 아까웠기 때문에  
나같은 사람을 위해서라도 삽질을 줄이는 순서를 공유해야겠다고 마음먹었다(..)

[지킬문서](https://jekyllrb-ko.github.io/)에 나온 가이드가 잘 번역이 되어있지만  
초보자로써 바로 따라하기 힘든점은 있었다.
- 루비 써본적 없음
- 정적 블로그 생성 해본적 없음
- 커맨드 명령어 잘 모름

이런 이유로 구글링 해서 나온 글을 봐도 한번에 깔끔하게 따라하지 못하고 비슷한 실수를 여러번 반복하게 되었다.   
~~공식문서에서는 단 몇초만에 된다고 쓰여있지만 몇시간이 걸렸다~~  

최대한 실수를 줄일수 있는 순서를 이 글을 통해 공유 하고자 한다.  
이 순서만 하나씩 따라하면 지킬 블로그 만들기를 큰 무리 없이 진행 할 수 있다.  
1. [github](https://github.com/)에서 `xxxx.github.io` 라는 이름의 repository를 생성한다.  
2. 윈도우용 git클라이언트 혹은 편집도구를 통해 **1**에서 생성한 빈 경로 `xxxx.github.io`를 내려받는다.  
나는 윈도우용 [GitHub Desktop](https://desktop.github.com/)을 통해 내려받았다.  
3. [지킬문서](https://jekyllrb-ko.github.io/)에 나와있는 안내대로 윈도우용 루비 인스톨러 [RubyInstaller for Windows](https://rubyinstaller.org/) 를 설치한다.
4. **3**을 설치하면 실행되는 CommandPrompt창에 아래의 명령어를 친다.
```
gem install bundler jekyll
```
5. CommandPrompt창에서 **2**에서 내려받았던 경로로 이동한다. 내 경우 D드라이브 아래의 develop폴더로 접근해야했다. 그래서 아래처럼 이동을했다.
```
cd /d D:\
cd develop
cd xxxx.github.io
```
6. 위 명령어로 github에서 내려받은 폴더에 도착했다면, 이곳에서 jekyll을 실행하여 블로그를 생성한다. (마지막 마침표도 명령어임.)
```
jekyll new .
```
`xxxx.github.io` 폴더내에 자동적으로 이것저것 파일이 생성된것이 보일것이다.  
**6**번까지 완료했다면 이제 기본세팅이 완료된 **지킬 블로그를 로컬에서 확인 해 볼수있다.**  
CommandPrompt창에 `jekyll serve -w`라고 입력한 뒤  
인터넷 브라우저를 열어서 `http://localhost:4000` 을 열어보면 블로그 첫화면을 확인 할 수 있다!  
- 만약 이 때 빌드에러가 발생했다면 CommandPrompt창에 `bundle`이라고 입력 한 뒤  
 `jekyll serve -w`를 재시작을 해보면 해결될 때가 있다.  
- 또는 특정 gem파일을 찾을수 없다고 나오는 경우, 예를들어 **jekyll-feed**를 찾을 수 없다고 나오면  
`gem install jekyll-feed` 라고 입력 해 본다.

7. `xxxx.github.io` 폴더에 생성된 파일들을 github에 push해준다.  
(난 [GitHub Desktop](https://desktop.github.com/)를 통해 master branch에 push했다.)  
⭐️이 때 **주의할 점**은 폴더 내의 **Gemfile**을 반드시 함께 push해 주어야 한다는 점이다.  
해당 파일이 github에 함께 push되어야 지킬 블로그가 빌드되며 페이지가 열리게 된다!
8. ✔️마지막으로 인터넷 브라우저에서 `xxxx.github.io`를 접속 해 본다.
  
여러번 헤메인 끝에 이 절차를 이해 할 수 있게 되었다.  
나처럼 지킬 블로그 생성에 전체적으로(?) 어려움을 겪고있는 사람에게 도움이 되었으면 좋겠다. ^.^
