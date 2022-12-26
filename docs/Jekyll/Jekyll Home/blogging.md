---
layout: default
title: Blogging
nav_order: 8
parent: Jekyll Home
grand_parent: Jekyll
---
# Blogging

데이터베이스 없이 블로그를 가질 수 있는 방법이 궁금 할 것입니다. 진정한 지킬 스타일에서 블로깅은 텍스트 파일로만 구동됩니다.

## Posts

블로그 post은 **_posts**라는 폴더에 있습니다. post의 파일 이름은 게시 날짜, 제목, 확장자와 같은 특별한 형식을 갖습니다.    
`_posts / 2018-08-20-bananas.md` 에 다음 내용으로 첫 번째 post을 작성하십시오.

```markdown
---
layout: post
author: jill
---
A banana is an edible fruit – botanically a berry – produced by several kinds
of large herbaceous flowering plants in the genus Musa.

In some countries, bananas used for cooking may be called "plantains",
distinguishing them from dessert bananas. The fruit is variable in size, color,
and firmness, but is usually elongated and curved, with soft flesh rich in
starch covered with a rind, which may be green, yellow, red, purple, or brown
when ripe.
```

이것은 *작성자*와 *다른 레이아웃*이 있다는 점을 제외하고는 이전에 만든 `about.md` 와 같습니다. `author`는 사용자 지정 변수이며 필수는 아니며 `creator`와 같은 이름으로 지정될 지도 모르겠다.

## Layout

`post` 레이아웃이 존재하지 않으므로 **_layouts/post.html** 에서 다음 콘텐츠로 만들어야 합니다.   
다음은 레이아웃 상속의 예입니다. post 레이아웃은 제목, 날짜, 작성자 및 콘텐츠 본문을 출력하며 기본 레이아웃으로 래핑됩니다.    
또한 `date_to_string` 필터를 사용하면 날짜가 더 좋은 형식으로 지정됩니다.

{% raw %}
```liquid
---
layout: default
---
<h1>{{ page.title }}</h1>
<p>{{ page.date | date_to_string }} - {{ page.author }}</p>

{{ content }}
```
{% endraw %}


## List posts

현재 블로그 post로 이동할 수 있는 방법은 없습니다.   
일반적으로 블로그에는 모든 post을 나열하는 페이지가 있으며 다음에 수행하겠습니다.   
지킬은 `site.posts`에서 post을 제공합니다. 다음 내용으로 루트(**/blog.html**)에 `blog.html`를 만듭니다.

{% raw %}
```liquid
---
layout: default
title: Blog
---
<h1>Latest Posts</h1>

<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p>{{ post.excerpt }}</p>
    </li>
  {% endfor %}
</ul>
```
{% endraw %}

이 코드에는 몇 가지 주의해야 할 사항이 있습니다.    

* `post.url`은 Jekyll에 의해 post의 출력 경로로 자동 설정됩니다. 
* `post.title`은 post 파일 이름에서 가져오며 front matter의 `title`을 설정하여 override할 수 있습니다. 
* `post.excerpt`는 기본적으로 내용의 첫 번째 단락입니다.    

main navigation (기본 탐색)을 통해 이 페이지로 이동하는 방법도 필요합니다. **_data/navigation.yml**을 열고 블로그 페이지에 대한 항목을 추가합니다.

```yaml
- name: Home
  link: /
- name: About
  link: /about.html
- name: Blog
  link: /blog.html
```

## More posts

블로그는 하나의 post로 별로 흥미롭지 않습니다. 몇 가지 더 추가하십시오.

`_posts/2018-08-21-apples.md`:

```markdown
---
layout: post
author: jill
---
An apple is a sweet, edible fruit produced by an apple tree.

Apple trees are cultivated worldwide, and are the most widely grown species in
the genus Malus. The tree originated in Central Asia, where its wild ancestor,
Malus sieversii, is still found today. Apples have been grown for thousands of
years in Asia and Europe, and were brought to North America by European
colonists.
```

`_posts/2018-08-22-kiwifruit.md`:

```markdown
---
layout: post
author: ted
---
Kiwifruit (often abbreviated as kiwi), or Chinese gooseberry is the edible
berry of several species of woody vines in the genus Actinidia.

The most common cultivar group of kiwifruit is oval, about the size of a large
hen's egg (5–8 cm (2.0–3.1 in) in length and 4.5–5.5 cm (1.8–2.2 in) in
diameter). It has a fibrous, dull greenish-brown skin and bright green or
golden flesh with rows of tiny, black, edible seeds. The fruit has a soft
texture, with a sweet and unique flavor.
```

<a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a> 열고 블로그 post을 살펴보십시오.    
다음으로 각 post 작성자에 대한 페이지를 만드는 데 중점을 둘 것입니다.