---
layout: post
comments: true
title:  "github로 블로그 시작하기 : (1) Jekyll 은 어떤 방식으로 동작하는 걸까?"
date: 2017-06-21 00:00:00 +0000
description: Jekyll은 github로 블로그를 만들 때 사용자가 손쉽게 시작할 수 있도록 여러가지 기능들을 제공한다. Jekyll이라는 녀석이 어떻게 구성되어있고 어떤 방식으로 동작하는 지에 대한 이야기를 풀어본다.
categories: routine programming
---

## 1. Introduction
---
이전 포스트 ["github로 블로그 시작하기 : github + jekyll + bootstrap3"](https://nashory.github.io/routine/programming/2017/06/16/1_starting_blog_with_github.html)에는 `Jekyll` 을 이용해서 어떻게 `github`블로그를 만들 수 있는지 자세한 내용이 소개되어있는 블로그를 모아놓았다. Jekyll은 블로그를 만드는데 요즘 워낙 많이 쓰이는 툴이기도 하면서 그 자세한 내용이 하나하나 소개된 곳이 많기 때문에 본 포스트에서는 어떻게 Jekyll을 github 블로그에 적용시키는지 보다는 `Jekyll 이라는 툴이 어떻게 동작하는지` 그 원리에 대해 파악해 보려 한다. 실제로 나 역시 처음에는 각종 블로그에 소개된 대로 이미 만들어진 Jekyll 테마를 적용해서 블로그를 처음 시작했지만 마음에 안드는 구석들을 하나하나 수정하다보니 지금은 거의 처음 부터 뜯어 고쳤다고 해도 과언이 아니다. 그 과정에서 `Jekyll` 이라는 녀석이 어떻게 동작하는 지에 대해 알게된 내용을 정리해본다.

## 2. Jekyll이란 무엇인가?
`Jekyll`이란 개발자들이 애용하는 `github`에서 개발한 툴로 또다른 사이트 개발 툴인 워드프레스(Wordpress)의 가장 큰 경쟁자로 성장한 듯 하다.
이러한 `Jekyll`의 핵심 역할은 `텍스트 변환 엔진`이라고 할 수 있다. 즉, `HTML, Markdown` 등의 마크업 언어로 글을 작성하면 이것을 미리 정의해 놓은 규칙에 따라 다양한 레이아웃으로 포장하여 정적 웹사이트를 만들어 준다. 이 과정에서 사용자는 `_config.yml` 이나 `_posts` 폴더 등의 수정 또는 파일 추가를 통해 원하는 기능을 구현할 수 있다.

이때 우리는 `Jekyll`로 만드는 블로그들이 `정적 웹사이트`라는 데에 주목해야한다. `정적 웹사이트(Static website)`로 웹사이트를 구성하게 되면 PHP 언어를 이용한 서버 소프트웨어가 필요없이 HTML/CSS 등의 정적파일 만으로 사이트를 생성하므로 **매우 빠르고 가볍다.** `Jekyll`은 기본적으로 Markdown 언어로 작성한 포스트 글을 github에서 `commit & push` 하는 방식을 취하고 있기 때문에 `github`에 익숙하지 않은 사용자라면 다소 진입 장벽이 느껴질수 는 있겠지만, 로컬 저장소에 블로그를 통째로 저장해 놓고 원할때 Markdown만으로 블로그 글 작성이 가능해서 한번 익숙해지면 아주 매력적인 툴이 된다. (github에 commit 하고 push 할 때의 희열도 같이 느낄수 있다...)

## 3. 디렉토리 구조
먼저 `Jekyll`의 디렉토리 구조에 대해 살펴보자. 개인적으로는 `Jekyll`의 디렉토리 구조만 대충 알아도 거의 50% 이상은 알게 된 셈이라고 생각할 정도로 `Jekyll`은 직관적이고 쉽다. 먼저 [Jekyll 기반의 GitHub Pages에 블로그 만들기](https://xho95.github.io/blog/github/jekyll/git/2016/01/11/Make-a-blog-with-Jekyll.html)를 참고해서 `github`에 `Jekyll`기반의 블로그를 처음 만들면, `_includes, _layouts, _posts, _site, _config.yml`등과 같은 기본적인 파일등이 생성 된다. 이 폴더와 파일들은 _레이아웃을 정의하거나, 포스트 글을 저장하거나, 플러그인 할 코드 등을 저장_ 하는 등 각각 그 역할이 미리 정해져 있다. 그 역할이 뭔지만 잘 알아도 Jekyll로 만들어진 블로그 소스코드를 분석하는데 훨씬 수월하다.

<br/>
<table>
    <tr>
        <td><strong>파일/디렉토리</strong></td>  
        <td><strong>기능 & 역할</strong></td>
    </tr>
    <tr>
        <td>`_includes`</td>
        <td>이러이러한 역할이다.</td>
    </tr>
    <tr>
        <td>`_posts`</td>
        <td>이러이러한 역할이다.</td>
    </tr>
    <tr>
        <td>`__layouts`</td>
        <td>이러이러한 역할이다.</td>
    </tr>
    <tr>
        <td>`_site`</td>
        <td>이러이러한 역할이다.</td>
    </tr>
    <tr>
        <td>`_sass`</td>
        <td>이러이러한 역할이다.</td>
    </tr>
    <tr>
        <td>`_config.yml`</td>
        <td>환경 설정 정보를 저장한다. C 언어로 치면 Header 파일에 해당한다고 볼 수도 있겠다. <strong>url, title, emai</strong>등 공통으로 쓰이는 변수들을 저장해 놓을 수 있고, <strong>pagenate, markdown 환경</strong> 등 실제로 어떤 환경에서 작업 할 것인지 옵션을 설정 할 수도 있다. (다른 github 블로그에서 참고해서 작성해두면 편하다.)</td>
    </tr>
    <tr>
        <td>`sitemap.xml`</td>
        <td>이러이러한 역할이다.</td>
    </tr>
</table>











**References**
- [디렉토리 구조](http://jekyllrb-ko.github.io/docs/structure/)
- [Jekyll 기반의 GitHub Pages에 블로그 만들기](https://xho95.github.io/blog/github/jekyll/git/2016/01/11/Make-a-blog-with-Jekyll.html)
