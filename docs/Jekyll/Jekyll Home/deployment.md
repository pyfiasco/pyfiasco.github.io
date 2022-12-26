---
layout: default
title: Deployment
nav_order: 10
parent: Jekyll Home
grand_parent: Jekyll
---

# Deployment(배포)
{: .toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Gemfile

<!-- It's good practice to have a [Gemfile](/docs/ruby-101/#gemfile) for your site.
This ensures the version of Jekyll and other gems remains consistent across
different environments.

Create `Gemfile` in the root with the following: -->

사이트에 Gemfile을 사용하는 것이 좋습니다. 이렇게 하면 Jekyll 및 기타 gem의 버전이 다양한 환경에서 일관되게 유지됩니다. 다음을 사용하여 루트에 Gemfile을 만듭니다.

```ruby
source 'https://rubygems.org'

gem 'jekyll'
```

<!-- Then run `bundle install` in your terminal. This installs the gems and
creates `Gemfile.lock` which locks the current gem versions for a future
`bundle install`. If you ever want to update your gem versions you can run
`bundle update`.

When using a `Gemfile`, you'll run commands like `jekyll serve` with
`bundle exec` prefixed. So the full command is: -->

그런 다음 터미널에서 `bundle install`를 실행하십시오. 그러면 젬이 설치되고 향후 `bundle install`를 위해 현재 젬 버전을 잠그는 `Gemfile.lock`이 생성됩니다. 젬 버전을 업데이트하려면 `bundle update`를 실행할 수 있습니다.    
Gemfile을 사용할 때 `bundle exec` 접두사가 붙은 `jekyll serve`와 같은 명령을 실행합니다. 따라서 전체 명령은 다음과 같습니다.

```sh
bundle exec jekyll serve
```

<!-- This restricts your Ruby environment to only use gems set in your `Gemfile`. -->

이렇게 하면 `Gemfile`에 설정된 젬만 사용하도록 Ruby 환경이 제한됩니다.

## Plugins

<!-- Jekyll plugins allow you to create custom generated content specific to your
site. There's many  available or you can even
write your own. -->

Jekyll 플러그인을 사용하면 사이트에 특정한 사용자 정의 생성 콘텐츠를 만들 수 있습니다.    
사용 가능한 [plugins]({% link docs/Jekyll/Jekyll Home/Jekyll_docs/plugins.md %})이 많거나 직접 작성할 수도 있습니다.

<!-- There's three official plugins which are useful on almost any Jekyll site: -->
거의 모든 Jekyll 사이트에서 유용한 세 가지 공식 플러그인이 있습니다.  

<!-- * [jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap) - Creates a sitemap
file to help search engines index content
* [jekyll-feed](https://github.com/jekyll/jekyll-feed) - Creates an RSS feed for
your posts
* [jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag) - Adds meta tags to help
with SEO -->


  

* [jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap) - engines index content을 찾는 것을 돕는 sitemap 파일을 만든다.
* [jekyll-feed](https://github.com/jekyll/jekyll-feed) - post용 RSS feed를 만듭니다.
* [jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag) - SEO에 도움이되는 메타 태그를 추가합니다.

먼저 이것을 사용하려면 `Gemfile`에 추가해야합니다.    
`jekyll_plugins` 그룹에 넣으면 자동으로 Jekyll에 필요하게 됩니다.


```ruby
source 'https://rubygems.org'

gem 'jekyll'

group :jekyll_plugins do
  gem 'jekyll-sitemap'
  gem 'jekyll-feed'
  gem 'jekyll-seo-tag'
end
```

그리고  `_config.yml`에 다음 라인을 더한다:

```yaml
plugins:
  - jekyll-feed
  - jekyll-sitemap
  - jekyll-seo-tag
```

<!-- Now install them by running a `bundle update`.

`jekyll-sitemap` doesn't need any setup, it will create your sitemap on build.

For `jekyll-feed` and `jekyll-seo-tag` you need to add tags to
`_layouts/default.html`: -->

이제 `bundle update`를 실행하여 그들을 설치하십시오.    
`jekyll-sitemap`은 설정이 필요하지 않으며 빌드시 사이트 맵을 생성합니다.    
`jekyll-feed` 및 `jekyll-seo-tag`의 경우 `_layouts/default.html` 에 태그를 추가해야합니다.

{% raw %}
```liquid
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
    <link rel="stylesheet" href="/assets/css/styles.css">
    {% feed_meta %}
    {% seo %}
  </head>
  <body>
    {% include navigation.html %}
    {{ content }}
  </body>
</html>
```
{% endraw %}

<!-- Restart your Jekyll server and check these tags are added to the `<head>`. -->

Jekyll 서버를 다시 시작하고 이 태그가 `<head>`에 더해졌는지 체크하라.

## Environments

<!-- Sometimes you might want to output something in production but not
in development. Analytics scripts are the most common example of this.

To do this you can use [environments](/docs/configuration/environments/). You
can set the environment by using the `JEKYLL_ENV` environment variable when
running a command. For example: -->


때로는 프로덕션에서는 출력하고 싶지만 개발 중에는 출력하지 않을 수도 있습니다. 분석 스크립트가 가장 일반적인 예입니다. 이를 위해 [environments]({% link docs/Jekyll/Jekyll Home/Jekyll_docs/environments.md %})을 사용할 수 있습니다. 명령을 실행할 때 `JEKYLL_ENV` 환경 변수를 사용하여 환경을 설정할 수 있습니다. 예를 들어:

```sh
JEKYLL_ENV=production bundle exec jekyll build
```
<!-- 
By default `JEKYLL_ENV` is development. The `JEKYLL_ENV` is available to you
in liquid using `jekyll.environment`. So to only output the analytics script
on production you would do the following: -->

기본적으로 `JEKYLL_ENV`는 개발입니다. `JEKYLL_ENV`은 `jekyll.environment`를 사용하여 liquid에서 사용할 수 있습니다. 따라서 프로덕션에서만 분석 스크립트를 출력하려면 다음을 수행합니다.



{% raw %}
```liquid
{% if jekyll.environment == "production" %}
  <script src="my-analytics-script.js"></script>
{% endif %}
```
{% endraw %}

## Deployment

<!-- The final step is to get the site onto a production server. The most basic way
to do this is to run a production build: -->

마지막 단계는 사이트를 프로덕션 서버로 가져오는 것입니다. 이 작업을 수행하는 가장 기본적인 방법은 프로덕션 빌드를 실행하는 것입니다.

```sh
JEKYLL_ENV=production bundle exec jekyll build
```

<!-- And copy the contents of `_site` to your server.

A better way is to automate this process using a [CI](/docs/deployment/automated/)
or [3rd party](/docs/deployment/third-party/). -->

그리고  `_site`의 내용을 서버에 복사하십시오. 더 좋은 방법은 [CI](https://jekyllrb-ko.github.io/docs/deployment/automated/)
, [3rd party](https://jekyllrb-ko.github.io/docs/deployment/third-party/)를 사용하여 이 프로세스를 자동화하는 것입니다.

## Wrap up

<!-- That brings us to the end of this step-by-step tutorial and the beginning of
your Jekyll journey!

* Come say hi to the [community forums](https://talk.jekyllrb.com)
* Help us make Jekyll better by [contributing](/docs/contributing/)
* Keep building Jekyll sites! -->

* [community forums](https://talk.jekyllrb.com)
* [contributing](https://jekyllrb-ko.github.io/docs/contributing/)


# 배포 상세

ekyll 을 사용해 빌드한 사이트는 그 결과물의 정적인 특성 덕분에 여러가지 방법으로 배포할 수 있습니다. 여기 가장 보편적인 방법 몇 가지를 소개합니다:

## [수동](/docs/deployment/manual/)
## [자동](/docs/deployment/automated/)
## [서드 파티](/docs/deployment/third-party/)