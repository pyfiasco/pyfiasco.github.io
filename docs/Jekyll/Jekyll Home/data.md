---
layout: default
title: Data
nav_order: 6
parent: Jekyll Home
grand_parent: Jekyll
---
# Data

<!--
Jekyll supports loading data from YAML, JSON, and CSV files located in a `_data`
directory. Data files are a great way to separate content from source code to
make the site easier to maintain.
-->
Jekyll 은 `_data` 디렉토리에 있는 YAML, JSON, CSV 파일로 부터 데이터를 loading하는 기능을
제공합니다. 데이터 파일은 소스 코드로부터 컨텐츠를 분리하는 아주 좋은 방법으로서
사이트 유지/관리를 쉽게 만들어줍니다.

<!--
In this step you'll store the contents of the navigation in a data file
and then iterate over it in the navigation include.
-->
이 단계에서는 데이터 파일에 네비게이션의 컨텐츠를 저장한 뒤 navigation include에서 반복문을 구동합니다.

<!--
## Data file usage
-->
## 데이터 파일 사용법

<!--
[YAML](http://yaml.org/) is a format that's common in the Ruby ecosystem. You'll
use it to store an array of navigation items each with a name and link.
-->
[YAML](http://yaml.org/) 은 Ruby 생태계에서 일반적인 형식입니다.
이름과 링크 각각으로 navigation item의 배열을 이 형식으로 저장해볼 것입니다.

<!--
Create a data file for the navigation at `_data/navigation.yml` with the
following:
-->
네비게이션을 위한 데이터 파일을 `_data/navigation.yml` 에 생성하고 다음 내용을
입력합니다:

```yaml
- name: Home
  link: /
- name: About
  link: /about.html
```

<!--
Jekyll makes this data file available to you at `site.data.navigation`. Instead
of outputting each link in `_includes/navigation.html`, now you can iterate over
the data file instead:
-->
Jekyll 은 `site.data.navigation` 으로 이 데이터 파일을 사용할 수 있게 만듭니다.
`_includes/navigation.html` 에서 각 링크들을 나열하는 대신, 데이터 파일을 반복문 처리하여 나열할 수 있습니다:

{% raw %}
```liquid
<nav>
  {% for item in site.data.navigation %}
    <a href="{{ item.link }}" {% if page.url == item.link %}style="color: red;"{% endif %}>
      {{ item.name }}
    </a>
  {% endfor %}
</nav>
```
{% endraw %}

include 태그를 사용해서 `_layouts/default.html` 에 네비게이션을 추가합니다:

{% raw %}
```liquid
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {% include navigation.html %}
    {{ content }}
  </body>
</html>
```
{% endraw %}


`_layouts/default.html` 에 네비게이션을 추가합니다:

{% raw %}
```liquid
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {% include navigation.html %}
    {{ content }}
  </body>
</html>
```
{% endraw %}

브라우저에서 <a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a>
를 열어 페이지 사이를 이동해봅니다.






<!--
The output will be exactly the same. The difference is you’ve made it easier to
add new navigation items and change the HTML structure.
-->
완벽하게 include 사용 결과와 동일한 결과를 얻을 수 있습니다. 바뀐 것은 새 네비게이션 항목을 추가하고
HTML 구조를 변경하는 일이 쉬워졌다는 것입니다.

<!--
What good is a site without CSS, JS and images? Let’s look at how to handle
assets in Jekyll.
-->
<!-- 사이트에 CSS 나 JS, 그림도 없이 뭐가 좋겠어요? 이런 에셋들을 Jekyll 에서
다루는 방법을 알아봅시다. -->
