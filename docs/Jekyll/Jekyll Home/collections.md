---
layout: default
title: Collections
nav_order: 9
parent: Jekyll Home
grand_parent: Jekyll

---
# Collections
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<!-- Let's look at fleshing out authors so each author has their own page with a
blurb and the posts they've published.

To do this you'll use collections. Collections are similar to posts except the
content doesn't have to be grouped by date. -->
author를 구체화하는 방법을 살펴 보겠습니다. 각 author는 게시한 광고 문구, post가 있는 `자체 페이지`를 갖습니다.     
이렇게 하려면 컬렉션을 사용합니다.    
컬렉션은 콘텐츠를 날짜별로 그룹화할 필요가 없다는 점을 제외하면 post과 비슷합니다.

## Configuration(설정)

<!-- To set up a collection you need to tell Jekyll about it. Jekyll configuration
happens in a file called `_config.yml` (by default).

Create `_config.yml` in the root with the following: -->
컬렉션을 설정하려면 Jekyll에게 알려야합니다. Jekyll configuration은 **_config.yml** (기본값)이라는 파일에서 이루어진다.    
다음을 사용하여 루트에 `_config.yml`을 만듭니다.


```yaml
collections:
  authors:
```

<!-- To (re)load the configuration, restart the jekyll server. Press `Ctrl`+`C` in your terminal to stop the server, and then `jekyll serve` to restart it. -->

configuration을 (다시)로드하려면 jekyll 서버를 다시 시작하십시오. 터미널에서 `Ctrl`+`C`를 눌러 서버를 중지한 후 `jekyll serve`로 다시 시작합니다.

## Add authors( author 추가 )

<!-- Documents (the items in a collection) live in a folder in the root of the site
named  _*collection_name*. In this case, `_authors`.

Create a document for each author: -->

문서(collection 대상 항목)는  사이트의 루트에 있는 폴더( *_collection-name*형식 - 이 경우 **_authors** )에 생성한다.     
각 author에 대한 문서를 만듭니다.

`_authors/jill.md`:

```markdown
---
short_name: jill
name: Jill Smith
position: Chief Editor
---
Jill is an avid fruit grower based in the south of France.
```

`_authors/ted.md`:

```markdown
---
short_name: ted
name: Ted Doe
position: Writer
---
Ted has been eating fruit since he was baby.
```

## Staff page ( 직원 페이지 )

<!-- Let's add a page which lists all the authors on the site. Jekyll makes the
collection available at `site.authors`.

Create `staff.html` and iterate over `site.authors` to output all the staff: -->

사이트의 모든 author를 나열하는 페이지를 추가해 보겠습니다. Jekyll은 이 컬렉션을 `site.authors`에서 이용할 수 있도록 합니다. **staff.html** 을 만들고 `site.author`를 반복하여 모든 직원을 출력합니다.


{% raw %}
```liquid
---
layout: default
title: Staff
---
<h1>Staff</h1>

<ul>
  {% for author in site.authors %}
    <li>
      <h2>{{ author.name }}</h2>
      <h3>{{ author.position }}</h3>
      <p>{{ author.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>
```
{% endraw %}

<!-- Since the content is markdown, you need to run it through the
`markdownify` filter. This happens automatically when outputting using
{% raw %}`{{ content }}`{% endraw %} in a layout.

You also need a way to navigate to this page through the main navigation. Open
`_data/navigation.yml` and add an entry for the staff page: -->

콘텐츠가 마크다운이므로 `markdownify` 필터를 통해 실행해야 합니다. 레이아웃에서 {% raw %}`{{ content }}`{% endraw %}를 사용하여 출력할 때 자동으로 발생합니다.    
기본 탐색을 통해 이 페이지로 이동하는 방법도 필요합니다. **_data/navigation.yml**을 열고 직원 페이지에 대한 항목을 추가합니다.


```yaml
- name: Home
  link: /
- name: About
  link: /about.html
- name: Blog
  link: /blog.html
- name: Staff
  link: /staff.html
```

## Output a page ( 출력 페이지 )

<!-- By default, collections do not output a page for documents. In this case we
want each author to have their own page so let's tweak the collection
configuration.

Open `_config.yml` and add `output: true` to the author collection
configuration: -->

기본적으로 컬렉션은 문서에 대한 페이지를 출력하지 않습니다. 이 경우 각 author가 자신의 페이지를 갖기를 원하므로 컬렉션 설정을 조정해 보겠습니다. `_config.yml`을 열고 author collection에 **output: true**를  추가합니다.


```yaml
collections:
  authors:
    output: true
```

<!-- You can link to the output page using `author.url`.

Add the link to the `staff.html` page: -->

`author.url`을 사용하여 출력 페이지에 연결할 수 있습니다. `staff.html` 페이지에 링크를 추가합니다.

{% raw %}
```liquid
---
layout: default
title: Staff
---
<h1>Staff</h1>

<ul>
  {% for author in site.authors %}
    <li>
      <h2><a href="{{ author.url }}">{{ author.name }}</a></h2>
      <h3>{{ author.position }}</h3>
      <p>{{ author.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>
```
{% endraw %}

<!-- Just like posts you'll need to create a layout for authors.

Create `_layouts/author.html` with the following content:   --> 

post과 마찬가지로, author를 위한 레이아웃을 만들어야 합니다.    
다음 내용으로 **_layouts/author.html**를 만듭니다.

{% raw %}
```liquid
---
layout: default
---
<h1>{{ page.name }}</h1>
<h2>{{ page.position }}</h2>

{{ content }}
```
{% endraw %}

## Front matter defaults

<!-- Now you need to configure the author documents to use the `author` layout. You
could do this in the front matter like we have previously but that's getting
repetitive.

What you really want is all posts to automatically have the post
layout, authors to have author and everything else to use the default.

You can achieve this by using [front matter defaults](/docs/configuration/front-matter-defaults/)
in `_config.yml`. You set a scope of what the default applies to, then the
default front matter you'd like.

Add defaults for layouts to your `_config.yml`, -->

이제 `author` layout을 사용하도록 author document를 설정해야 합니다. 이전처럼 front matter에서 이 작업을 수행 할 수 있지만 반복된 작업입니다.    
당신이 정말로 원하는 것은 모든 post이 자동으로 post 레이아웃을 갖고, author가 author, 다른 모든 것은 기본값을 사용하도록 하는 것입니다.    

**_config.yml**에서 [front matter defaults]({% link docs/Jekyll/Jekyll Home/front matter.md %})을 사용하여 이 작업을 수행할 수 있습니다.    
기본값이 적용되어야 할 범위를 설정 한 다음, 원하는 기본 front matter을 설정합니다.   
_config.yml에 레이아웃 기본값을 추가하십시오.

```yaml
collections:
  authors:
    output: true

defaults:
  - scope:
      path: ""
      type: "authors"
    values:
      layout: "author"
  - scope:
      path: ""
      type: "posts"
    values:
      layout: "post"
  - scope:
      path: ""
    values:
      layout: "default"
```

<!-- Now you can remove layout from the front matter of all pages and posts. Note
that any time you update `_config.yml` you'll need to restart Jekyll for the
changes to take effect. -->

이제 모든 페이지와 post의 front matter에서 레이아웃을 제거 할 수 있습니다. `_config.yml`을 업데이트 할 때마다 변경 사항을 적용하려면 Jekyll을 다시 시작해야합니다.

## List author's posts

<!-- Let's list the posts an author has published on their page. To do
this you need to match the author `short_name` to the post `author`. You
use this to filter the posts by author.

Iterate over this filtered list in `_layouts/author.html` to output the
author's posts: -->
author가 자신의 페이지에 게시 한 post을 나열 해 보겠습니다. 이렇게 하려면 author `short_name` 과 post `author`을 일치시켜야 합니다. 이를 사용하여 author별로 post을 필터링합니다. **_layouts/author.html** 에서 이 필터링된 목록을 반복하여 author의 post을 출력합니다.

{% raw %}
```liquid
---
layout: default
---
<h1>{{ page.name }}</h1>
<h2>{{ page.position }}</h2>

{{ content }}

<h2>Posts</h2>
<ul>
  {% assign filtered_posts = site.posts | where: 'author', page.short_name %}
  {% for post in filtered_posts %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
```
{% endraw %}

## Link to authors page

<!-- The posts have a reference to the author so let's link it to the author's page.
You can do this using a similar filtering technique in `_layouts/post.html`: -->
post에는 author에 대한 참조가 있으므로 author의 페이지에 연결해 보겠습니다. `_layouts/post.html` 에서 유사한 필터링 기술을 사용하여이 작업을 수행 할 수 있습니다.

{% raw %}
```liquid
---
layout: default
---
<h1>{{ page.title }}</h1>

<p>
  {{ page.date | date_to_string }}
  {% assign author = site.authors | where: 'short_name', page.author | first %}
  {% if author %}
    - <a href="{{ author.url }}">{{ author.name }}</a>
  {% endif %}
</p>

{{ content }}
```
{% endraw %}

<!-- Open up <a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a> and
have a look at the staff page and the author links on posts to check everything
is linked together correctly.

In the next and final step of this tutorial, we'll add polish to the site and
get it ready for a production deployment. -->
<a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a>열고 직원 페이지와 post의 author 링크를 살펴보고 모든 것이 올바르게 연결되어 있는지 확인하십시오. 이 자습서의 다음 단계이자 마지막 단계에서는 사이트에 세련미를 추가하고 프로덕션 배포를 준비합니다.