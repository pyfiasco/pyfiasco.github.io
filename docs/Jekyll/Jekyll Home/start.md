---
layout: default
title: Jekyll Start
nav_order: 1
parent: Jekyll Home
grand_parent: Jekyll
---

# Jekyll start
{: toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<!--
Jekyll is written in Ruby. If you're new to Ruby, this page is to help you get
up to speed with some of the terminology.
-->
Jekyll 은 루비로 작성되었습니다. 루비를 처음 접한다면, 용어들에 빨리 익숙해지는데에
이 페이지가 도움이 될 것입니다.

<!--
## Gems
-->

## Gem

<!--
A gem is code you can include in Ruby projects. It allows you to package up functionality and share it across other projects or with other people. Gems can perform functionality such as:
-->
젬은 루비 프로젝트에 포함할 수 있는 코드입니다. 기능들을 패키지화해서 다른 사람들이나 프로젝트에 공유할 수 있게 해줍니다. 젬은 다음과 같은 기능을 수행할 수 있습니다:

<!--
* Converting a Ruby object to JSON
* Pagination
* Interacting with APIs such as GitHub
* Jekyll itself is a gem as well as many Jekyll plugins including
[jekyll-feed](https://github.com/jekyll/jekyll-feed),
[jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag) and
[jekyll-archives](https://github.com/jekyll/jekyll-archives).
-->
* 루비 오브젝트를 JSON 으로 변환
* 페이지 번호 매기기
* GitHub 과 같은 API 와 연동
* Jekyll 자체는 젬이다. (플러그인 포함)
  * [jekyll-feed](https://github.com/jekyll/jekyll-feed) 
  * [jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag)   
  * [jekyll-archives](https://github.com/jekyll/jekyll-archives)   

## Gemfile

<!--
A `Gemfile` is a list of gems required for your site. For a simple Jekyll site it might look something like this:
-->
`Gemfile` 은 site에 필요한 젬들의 목록입니다. 단순한 Jekyll site를 예로 들면 이렇게 생겼습니다:

```ruby
source "https://rubygems.org"

gem "jekyll"

group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
end
```

## Bundler

<!--
Bundler installs the gems in your `Gemfile`. It's not a requirement for you to use a `Gemfile` and `bundler` however it's highly recommended as it ensures you're running the same version of Jekyll and Jekyll plugins across different environments.
-->
Bundler 는 `Gemfile` 에 있는 젬들을 설치합니다. `Gemfile` 과 `bundler` 를 사용하는 것이 필수는 아니지만 여러 다른 환경에서 올바른 버전의 Jekyll 과 Jekyll 플러그인을 사용하게 도와주기 때문에 적극적으로 권장하고 있습니다.

<!--
`gem install bundler` installs [Bundler](https://rubygems.org/gems/bundler). You only need to install it once &mdash; not every time you create a new Jekyll project. Here are some additional details:
-->
`gem install bundler` 명령으로 [Bundler](https://rubygems.org/gems/bundler) 를 설치합니다. 이 설치는 한 번만 하면 됩니다 &mdash; Jekyll 프로젝트를 생성할 때마다가 아닙니다. 여기 세부사항이 몇 가지 더 있습니다:

<!--
If you're using a `Gemfile` you would first run `bundle install` to install the gems, then `bundle exec jekyll serve` to build your site. This guarantees you're using the gem versions set in the `Gemfile`. If you're not using a `Gemfile` you can just run `jekyll serve`.
-->
만약 `Gemfile` 을 사용하고 있다면 먼저 `bundle install` 을 실행해 젬들을 설치하고, `bundle exec jekyll serve` 로 site를 빌드합니다. 이는 `Gemfile` 에 설정된 버전의 젬들을 사용하도록 보장해줍니다. `Gemfile` 을 사용하지 않는다면 그냥 `jekyll serve` 라고 실행하면 됩니다.

<!--
For more information about how to use Bundler in your Jekyll project, this [tutorial](/tutorials/using-jekyll-with-bundler/) should provide answers to the most common questions and explain how to get up and running quickly.
-->
당신의 Jekyll 프로젝트에 Bundler 를 사용하는 방법에 대한 더 자세한 내용을 원하는 경우, 이 [튜토리얼](https://jekyllrb-ko.github.io/tutorials/using-jekyll-with-bundler/)에 가장 흔히 묻는 질문들에 대한 답변과 빠르게 준비를 끝내고 실행하는 방법이 설명되어 있습니다.


# 설치
{: .toc}

<!-- #title: Installation
title: 
description: Official guide to install Jekyll on macOS, GNU/Linux or Windows.
permalink: /docs/installation/ -->

<!--
Jekyll is a [Ruby Gem](/docs/ruby-101/#gems) that can be installed on most systems.
-->
Jekyll 은 [루비 젬](https://jekyllrb-ko.github.io/docs/ruby-101/#gems)이며, 거의 모든 시스템에 설치할 수 있습니다.

<!--
## Requirements
-->
## 준비물 {#requirements}

<!--
* [Ruby](https://www.ruby-lang.org/en/downloads/) version **{{ site.data.ruby.min_version }}** or above, including all development headers (ruby version can be checked by running `ruby -v`)
* [RubyGems](https://rubygems.org/pages/download) (which you can check by running `gem -v`)
* [GCC](https://gcc.gnu.org/install/) and [Make](https://www.gnu.org/software/make/) (in case your system doesn't have them installed, which you can check by running `gcc -v`,`g++ -v`  and `make -v` in your system's command line interface)
-->
* [루비](https://www.ruby-lang.org/en/downloads/) 버전 **{{ site.data.ruby.min_version }}** 또는 그 이상. 모든 개발환경 헤더 포함 (루비 버전은 `ruby -v` 로 확인할 수 있습니다)
* [루비젬](https://rubygems.org/pages/download) (명령어 `gem -v` 로 확인할 수 있습니다)
* [GCC](https://gcc.gnu.org/install/) 와 [Make](https://www.gnu.org/software/make/) (시스템에 설치 되어있지 않는 경우. 명령행 인터페이스에서 `gcc -v`, `g++ -v` 그리고 `make -v` 로 확인할 수 있습니다)

<!--
## Guides
-->
## 가이드 {#guides}

<!--
For detailed install instructions have a look at the guide for your operating system.
-->
세부적인 절차는 자신의 운영체제에 해당하는 가이드를 확인해보세요.

<!--
* [macOS](/docs/installation/macos/)
* [Ubuntu Linux](/docs/installation/ubuntu/)
* [Other Linux distros](/docs/installation/other-linux)
* [Windows](/docs/installation/windows/)
-->
<!-- * [맥OS](/docs/installation/macos/)
* [우분투 리눅스](/docs/installation/ubuntu/)
* [다른 리눅스 배포판](/docs/installation/other-linux) -->
* [윈도우즈](https://jekyllrb-ko.github.io/docs/installation/windows/)

# 커뮤니티
<!-- ---
#title: Community
title: 커뮤니티
permalink: /docs/community/
redirect_from: "/help/index.html"
--- -->

<!--
## Jekyll Contributor Code of Conduct
-->
<!-- ## Jekyll 기여자 행동규칙 -->

<!--
As contributors and maintainers of this project, and in the interest of fostering an open and welcoming community, we pledge to respect all people who contribute through reporting issues, posting feature requests, updating documentation, submitting pull requests or patches, and other activities.
-->
<!-- 이 프로젝트의 기여자 또는 관리자로서, 그리고 개방적이고 다정한 커뮤니티를 조성하기 위하여, 우리는 문제점 보고, 추가기능 제안, 문서 갱신, Pull Request 나 패치를 보내거나 그 밖의 어떠한 활동으로든 기여하는 모든 이들을 존중할 것을 약속합니다. -->

<!--
Read the full [code of conduct](/docs/conduct/)
-->
<!-- [행동규칙](/docs/conduct/) 전문을 읽어보시기 바랍니다. -->

<!--
## Where to get support
-->
## 도움을 받을 수 있는 곳

<!--
If you're looking for support for Jekyll, there are a lot of options:
-->
Jekyll 에 관련된 도움을 찾고 있다면, 선택지가 몇 가지 있습니다:

<!--
* Read the [Jekyll Documentation](https://jekyllrb.com/docs/)
* If you have a question about using Jekyll, start a discussion on the [Jekyll Forum](https://talk.jekyllrb.com/) or [StackOverflow](https://stackoverflow.com/questions/tagged/jekyll)
* Chat with Jekyllers &mdash; Join our [Gitter channel](https://gitter.im/jekyll/jekyll) or our [IRC channel on Freenode](irc:irc.freenode.net/jekyll)
-->
* [Jekyll 포럼](https://talk.jekyllrb.com/)
* [StackOverflow](https://stackoverflow.com/questions/tagged/jekyll) 
* [Gitter 채널](https://gitter.im/jekyll/jekyll)
* [Freenode 의 IRC 채널](irc:irc.freenode.net/jekyll)

<!--
There are a bunch of helpful community members on these services that should be willing to point you in the right direction.
-->
<!-- 위 커뮤니티들의 수 많은 멤버들은 당신이 올바른 답을 찾을 수 있도록 기꺼이 도울 것입니다. -->

<!--
**Reminder: Jekyll's issue tracker is not a support forum.**
-->
<!-- **주목: Jekyll 의 이슈 트래커는 지원 포럼이 아닙니다.** -->

<!--
## Ways to contribute
-->
<!-- ## 기여하는 방법 -->

<!--
* [How to Contribute](/docs/contributing/)
* [How to file a bug](/docs/community/bug/)
* [Guide for maintaining Jekyll](/docs/maintaining/)
-->
<!-- * [기여하는 방법](/docs/contributing/)
* [버그 리포트 방법](/docs/community/bug/)
* [Jekyll 관리자 가이드](/docs/maintaining/) -->

<!-- ## Jekyllconf

<!--
[Watch videos](/jekyllconf/) from members of the Jekyll community speak about interesting use cases, tricks they’ve learned or meta Jekyll topics.
-->
<!-- Jekyll 커뮤니티 멤버들이 흥미로운 사용 사례와 그들이 발견한 트릭 또는 기타 Jekyll 관련 주제에 관해 이야기하는 [비디오](/jekyllconf/)를 살펴보세요. -->

<!--
## Jekyll on Twitter
-->
<!-- ## Jekyll 트위터 -->

<!--
The [official Jekyll Twitter account](https://twitter.com/jekyllrb).
-->
<!-- [공식 Jekyll 트위터 계정](https://twitter.com/jekyllrb). --> 

<!-- ---
layout: step
#title: Setup
title: 셋업
#menu_name: Step by Step Tutorial
menu_name: 단계별 튜토리얼
position: 1
--- -->
<!--
Welcome to Jekyll's step-by-step tutorial. The goal of this tutorial is to take
you from having some front end web development experience to building your
first Jekyll site from scratch — not relying on the default gem-based theme.
Let's get into it!
-->
Jekyll 단계별 튜토리얼에 오신 것을 환영합니다. 이 튜토리얼의 목표는 약간의
프론트엔드 웹 개발 경험을 쌓는 것부터 아무것도 없이 — 기본 젬 기반 테마에
의존하지 않고 — 시작해 당신의 첫 Jekyll 사이트를 생성하는 것입니다.
시작해봅시다!

<!--
## Installation
-->
# 설치 상세

<!--
Jekyll is a Ruby program so you need to install Ruby on your machine to begin
with. Head over to the [install guide](/docs/installation/) and follow the
instructions for your operating system.
-->
Jekyll 은 루비 프로그램이기 때문에 우선 루비를 설치해야 합니다.
[설치 설명서](https://jekyllrb-ko.github.io/docs/installation/)를 열어 자신의 운영체제에 맞는
지시를 따릅니다.

<!--
With Ruby setup you can install Jekyll by running the following in your
terminal:
-->
루비가 준비되었으면 터미널에 다음과 같이 실행하여 Jekyll 을 설치할 수
있습니다:

```sh
gem install jekyll bundler
```

<!--
To create a new `Gemfile` to list your project's dependencies run:
-->
프로젝트의 의존요소 목록인 `Gemfile` 을 생성하려면 이렇게 실행합니다:

```sh
bundle init
```

<!--
Now edit the `Gemfile` and add jekyll as a dependency:
-->
이제 `Gemfile` 을 열어 jekyll 을 의존요소로 추가합니다:

```ruby
gem "jekyll"
```

<!--
Finally run `bundle` to install jekyll for your project.
-->
마지막으로 `bundle` 을 실행해 프로젝트에 Jekyll 을 설치합니다.

<!--
You can now prefix all jekyll commands listed in this tutorial with `bundle exec`
to make sure you use the jekyll version defined in your `Gemfile`.
-->
이제부터 이 튜토리얼에 언급된 모든 Jekyll 명령어 앞에 `bundle exec` 를 붙여
실행하면 항상 `Gemfile` 에 정의된 버전의 Jekyll 을 사용할 수 있습니다.

<!--
## Create a site
-->
## 사이트 생성

<!--
It's time to create a site! Create a new directory for your site, you can name
it whatever you'd like. Through the rest of this tutorial we'll refer to this
directory as “root”.
-->
이제 사이트를 생성할 차례입니다! 사이트를 위한 새 디렉토리를 원하는 이름으로
생성합니다. 이 튜토리얼에서는 이 디렉토리를 “루트” 라고 부를 것입니다.

<!--
If you're feeling adventurous, you can also initialize a Git repository here.
One of the great things about Jekyll is there's no database. All content and
site structure are files which a Git repository can version. Using a repository
is completely optional but it's a great habit to get into. You can learn more
about using Git by reading through the
[Git Handbook](https://guides.github.com/introduction/git-handbook/).
-->
모험을 즐기는 편이라면, 여기에 Git 저장소를 구성할 수도 있습니다.
Jekyll 의 장점 중 하나는 데이터베이스가 없다는 것입니다. 컨텐츠와 사이트 구조는
모두 파일로 되어있어 Git 저장소로 버전관리가 가능합니다. 저장소를 사용하는 것은
전적으로 선택사항이지만 익숙해지면 좋은 습관임에는 틀림이 없습니다. Git 을
사용하는 방법에 대해 더 배우고 싶다면
[Git Handbook](https://guides.github.com/introduction/git-handbook/) 을 읽어보세요.

<!--
Let's add your first file. Create `index.html` in the root with the following
content:
-->
첫 번째 파일을 추가해봅시다. 루트에 다음과 같은 내용을 가진 `index.html` 을
생성합니다:

```html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Home</title>
  </head>
  <body>
    <h1>Hello World!</h1>
  </body>
</html>
```

<!--
## Build
-->
## 빌드

<!--
Jekyll is a static site generator so we need Jekyll to build the site
before we can view it. There are two commands you can run in the root of your site
to build it:
-->
Jekyll 은 정적 사이트 생성기로서 사이트를 보려면 먼저 Jekyll 로 사이트를
빌드해야 합니다. 사이트 빌드에 사용하는 명령어는 두 가지로 사이트의 루트에서
실행할 수 있습니다:

<!--
* `jekyll build` - Builds the site and outputs a static site to a directory
called `_site`.
* `jekyll serve` - Does the same thing except it rebuilds any time you make
a change and runs a local web server at `http://localhost:4000`.
-->
* `jekyll build` - 사이트를 빌드하고 `_site` 라는 디렉토리에 정적 사이트를
생성합니다.
* `jekyll serve` - 위와 동일한 작업을 하지만 추가로 내용이 변경되면 사이트를
다시 빌드하고 `http://localhost:4000` 주소에 로컬 웹 서버를 구동합니다.

<!--
When you're developing a site you'll use `jekyll serve` as it updates with any
changes you make.
-->
사이트 개발 중에는 `jekyll serve` 를 사용해 사이트를 수정할 때마다 갱신이 되도록
합니다.

<!--
Run `jekyll serve` and go to
<a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a> in
your browser. You should see "Hello World!".
-->
`jekyll serve` 를 실행하고 브라우저로
<a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a> 에
접속합니다. "Hello World!" 가 보일 것입니다.

<!--
Well, you might be thinking what's the point in this? Jekyll just copied an
HTML file from one place to another. Well patience young grasshopper, there's
still much to learn!
-->
음.. 이런 생각이 들 수도 있어요.<br/>
이런걸 왜 하고 있지? Jekyll 이 한 일이라곤 HTML 파일을 다른 위치로 그냥 복사한 것 뿐이네.<br/>
자.. 참을성이 필요한 때입니다. 아직 배울게 많아요!