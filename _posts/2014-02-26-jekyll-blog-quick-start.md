---
layout: post
title: "지킬로 블로그 시작하기"
tagline: "Jekyll Blog Quick Start"
description: "지킬로 블로그 시작하기"
category: "Jekyll"
tags: [Jekyll, Bootstrap, blog, 지킬, 부트스트랩, 블로그, 지킬부트스트랩]
---
{% include JB/setup %}
# Jekyll 지킬


### Jekyll 시작하기
어디선가 Jekyll은 워드프레스보다 훨씬 설치가 간단 하다고 하는데 그 말 그대로 github에 저장소를 만들고 터미널에서 몇 줄이면 바로 블로그가 생성 되었다. (보통 10여분 정도 걸리기도 한다고 하지만 대부분 바로 생성 되었다.)

```
$ jekyll new 저장소명  
$ cd 저장소명
$ git init
$ git remote add origin 저장소경로
$ git add .
$ git commit -m 'Initial commit'
$ git push origin master (프로젝트 페이지의 경우 부모가 없는 gh-pages브랜치를 만들어 push)
```

이 간단한 과정이면 블로그가 생성 되고 별도의 DB설정 없이 마크다운 문서를 바로 포스트할 수 있다. DB가 없는 게 조금 어색하기도 했지만 어짜피 로컬에서 쓰는 글도 대부분 마크다운 문서로 저장하고 있었기 때문에 오히려 관리는 더 편할거 같다는 생각이 들었다. (아직 많이 사용해 보진 않았지만) 블로그로 통계낼 것도 아니고 간단한 통계기능은 `구글어날리틱스`를 사용하면 되니 DB가 없더라도 불편할 일은 그닥 없을 거 같았다. 전문적인 블로그를 운영할 것도 아니고 개인적인 기록차원에서 사용할 것 이라면 더욱 더 말이다.

그리고 무엇보다도 호스팅에 신경쓰지 않아도 된다는 게 마음에 들었다. 그간 가상호스팅을 몇 년 간 사용하긴 했지만 사용 빈도도 적고 개인적인 학습 목적에서 사용하는 용도로는 아마존 EC2를 더 자주 사용했기 때문에 굳이 호스팅 비용을 들여가며 가상서버를 유지할 의지가 점점 줄어들어가고 있다.

지킬은 블로그가 아니라 파싱엔진이라고도 하지만 편하고 서버 유지 및 관리에 대한 부담 없이 사용하기 좋아서 쓰기로 마음 먹었다. 그리고 `루비`로 만들어졌다는 점도 마음에 들었다. 루비를 사용해 본적은 없지만 루비로 만들어진 [레드마인(Redmine)](http://www.redmine.org/)은 충분히 매력적이었기 때문에 루비에 대한 간이라도 보고 싶어졌다.

### 지킬 테마 고르기
일단 지킬을 설치하고 나니 테마를 직접 만들 의지와 여유가 없어서 사용할만한 테마를 골라야 했다. 워드프레스 처럼 다양하진 않지만 사용 해볼만한 테마가 몇가지 있긴 했지만 태그, 카테고리 등의 기능을 사용하기 위해선 별도의 플러그인을 필요로 해서 `지킬부트스트랩`([JekyllBootstrap](http://jekyllbootstrap.com/))을 사용하기로 마음 먹었다.
지킬부트스트랩엔 내가 최소로 원하는 기능인 카테고리, 태그, 아카이브, 덧글, 부트스트랩 테마 를 모두 포함하고 있어서 고민 없이 바로 클론 받아 로컬에서 이것저것 살펴봤다.
 


#### Jekyll theme 후보였던 것들
 - [Lanyon · A Jekyll theme](http://lanyon.getpoole.com/) - bootstrap을 개발한 [@mdo](https://twitter.com/mdo) 가 만든 테마로 페이스북 스타일의 햄버거? 아이콘이 있는 메뉴를 지원한다.
 - [HPSTR Theme](http://mmistakes.github.io/hpstr-jekyll-theme/) - 포스트별로 배경이미지를 바꿀 수 있다.


### 쓸데없는 시행착오 : gh-pages branch
 [Creating Project Pages manually · GitHub Help](https://help.github.com/articles/creating-project-pages-manually) 에 나와 있는 것처럼 부모가 없는 `gh-pages` branch에서 동작한다 하여 해당 브랜치를 만들었지만 마스터 브랜치에 반영이 되지 않으면 `username.github.io` 페이지에서 볼 수가 없었다.
 그래서 기본 branch를 master에서 gh-pages로 변경 했지만 역시나 보여지지 않았다.

 하지만 `username.github.com` root 저장소에 지킬을 설치할 경우 gh-pages 브랜치를 사용하지 않는 다는 걸 뒤늦게 알았다. 이미 [User, Organization and Project Pages · GitHub Help](https://help.github.com/articles/user-organization-and-project-pages)에서 읽었지만 프로젝트 페이지 도움말에서 이 내용이 내 머릿속에 덮어쓰기 되어버린 것이다. 프로젝트로 생성할 경우에만 gh-pages를 통해 디플로이 하면 된다고 나와 있는 걸 모든 github 페이지는 gh-pages에서 돌아간다고 생각한 게 잘못이었다. 제목에도 프로젝트 페이지라 나와 있건만 왜 삽질을 한 건지, 허무하게도 `username.github.com`의 master branch에서 지킬은 너무나도 잘 돌아갔다. 하지만 여러번의 삭제 재설치로 인해 github에 좀 더 익숙해 졌으니 그걸로 위안을 삼아야지, 



### Jekyll SEO
 - [Constantly Learning: Jekyll and SEO Optimization](http://bretthard.in/2012/06/jekyll-and-seo-optimization/)


### 참고한 Jekyll 사용기
 - [Jekyll 한국어 번역 사이트 • Simple, blog-aware, static sites](http://svperstarz.github.io/jekyll-docs-ko/)
 - [Spoqa Tech Blog- Spoqa 블로그 탄생 비화](http://spoqa.github.io/2011/12/17/about-spoqa-blog-creation.html)
 - [Jekyll을 이용해서 블로그 만들기 (1)](http://devblog.croquis.com/ko/2012/05/22/1-jekyll-blog.html) : jekyllbootstrap을 사용한 블로그 사용 후기
 - [#dogfeet - GitHub의 페이지 기능 이용하기](http://dogfeet.github.io/articles/2012/github-pages.html)
 - [hello jekyll! jekyll-bootstrap 이용한 블로그](http://ohyecloudy.com/ddiary/2013/09/21/hello-jekyll/) : pending branch에서 글을 쓰고 gh-pages 브랜치로 글을 발행 한다고 함
 - jekyll bootstrap : [The Quickest Way to Blog on GitHub Pages. | ruhoh universal static blog generator](http://jekyllbootstrap.com/)
 - [지킬로 깃허브에 무료 블로그 만들기 - Nolboo's Blog](http://nolboo.github.io/blog/2013/10/15/free-blog-with-github-jekyll/) : 지킬 설치 과정이 엄청 자세하다.


