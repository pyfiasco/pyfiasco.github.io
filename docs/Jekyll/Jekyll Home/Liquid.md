---
layout: default
title: Liquid
nav_order: 2
parent: Jekyll Home
grand_parent: Jekyll
---

# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<!--
Jekyll uses the [Liquid](https://shopify.github.io/liquid/) templating language
to process templates.
-->
Jekyll 은 [Liquid](https://shopify.github.io/liquid/) 템플릿 언어를
사용해 템플릿을 처리합니다.

<!--
Generally in Liquid you output content using two curly braces e.g.
{% raw %}`{{ variable }}`{% endraw %} and perform logic statements by
surrounding them in a curly brace percentage sign e.g.
{% raw %}`{% if statement %}`{% endraw %}. To learn more about Liquid, check
out the [official Liquid Documentation](https://shopify.github.io/liquid/).
-->
일반적으로 Liquid 에서는 contents를 출력할 때 중괄호 두 개를 사용하고 (예,
{% raw %}`{{ variable }}`{% endraw %})    
중괄호와 퍼센트 표시를 사용해서 논리 연산을 수행합니다 (예, {% raw %}`{% if statement %}`{% endraw %}).    


<!--
Liquid is where Jekyll starts to get more interesting. Liquid is a templating
language which has three main parts: [objects](#objects), [tags](#tags) and
[filters](#filters).
-->
Liquid 는 Jekyll 을 더 흥미롭게 만들어줍니다. Liquid 는 템플릿 언어로서
세 가지 부분으로 나눌 수 있습니다: [오브젝트](#오브젝트)와 [태그](#태그),
[필터](#필터).

<!--
## Objects
-->
## 오브젝트

<!--
Objects tell Liquid where to output content. They're denoted by double curly
braces: {% raw %}`{{`{% endraw %} and {% raw %}`}}`{% endraw %}. For example:
-->
오브젝트는 컨텐츠를 어디에 출력할 지 Liquid 에 알려줍니다. 두 개의 중괄호로
표시합니다: {% raw %}`{{`{% endraw %} 와 {% raw %}`}}`{% endraw %}. 예시:

{% raw %}
```liquid
{{ page.title }}
```
{% endraw %}

<!--
Outputs a variable called `page.title` on the page.
-->
페이지에 `page.title` 변수의 값을 출력합니다.

<!--
## Tags
-->
## 태그

<!--
Tags create the logic and control flow for templates. They are denoted by curly
braces and percent signs: {% raw %}`{%`{% endraw %} and
{% raw %}`%}`{% endraw %}. For example:
-->
태그는 템플릿의 논리 연산과 흐름을 제어합니다. 중괄호와 퍼센트 문자로
표시합니다: {% raw %}`{%`{% endraw %} 와
{% raw %}`%}`{% endraw %}. 예시:


{% raw %}
```liquid
{% if page.show_sidebar %}
  <div class="sidebar">
    sidebar content
  </div>
{% endif %}
```
{% endraw %}

<!--
Outputs the sidebar if `page.show_sidebar` is true. You can learn more about the
tags available to Jekyll [here](/docs/liquid/tags/).
-->
변수 `page.show_sidebar` 가 참인 경우에 사이드바를 출력합니다. Jekyll 에서 사용할
수 있는 태그에 대해 더 배우려면 [여기](/docs/Jekyll/Jekyll Home/Jekyll_docs/tags/)를 방문하세요.

<!--
## Filters
-->
## 필터

<!--
Filters change the output of a Liquid object. They are used within an output
and are separated by a `|`. For example:
-->
필터는 Liquid 오브젝트의 출력을 변화시킵니다. `|` 로 구분해서 오브젝트 안에
사용합니다. 예시:

{% raw %}
```liquid
{{ "hi" | capitalize }}
```
{% endraw %}

<!--
Outputs `Hi`. You can learn more about the filters available to Jekyll
[here](/docs/liquid/filters/).
-->
`Hi` 를 출력합니다. Jekyll 에서 사용할 수 있는 필터에 대해 더 배우려면
[여기](/docs/Jekyll/Jekyll Home/Jekyll_docs/filters)를 방문하세요.

<!--
## Use Liquid
-->
## Liquid 를 사용하세요

<!--
Now it's your turn, change the Hello World! on your page to output as lowercase:
-->
이제 당신 차례입니다. 페이지의 Hello World! 를 소문자로 출력해보세요:

{% raw %}
```liquid
...
<h1>{{ "Hello World!" | downcase }}</h1>
...
```
{% endraw %}

<!--
To get our changes processed by Jekyll we need to add [front matter](../03-front-matter/) to the top of the page:
-->

{: .note}
> Jekyll 이 위 내용을 처리하게 하려면 [Front matter]( /docs/Jekyll/Jekyll Home/front matter/ ) 를 페이지 맨 처음에 추가해야 합니다:

<!--
```yaml
---
# front matter tells Jekyll to process Liquid
---
```
-->
```yaml
---
# Front matter은 Jekyll 에게 Liquid 를 처리하라고 지시합니다
---
```

<!--
Our "Hello World!" will now be downcased on render.
-->
이제 "Hello World!" 는 소문자로 렌더링됩니다.

<!--
It may not seem like it now, but much of Jekyll's power comes from combining
Liquid with other features.
-->
지금은 아닌 것 같을 수도 있겠지만, 다른 기능들과 Liquid 를 조합하면 Jekyll 의
강점이 눈에 띄게됩니다.

<!--
In order to see the changes from `downcase` Liquid filter, we will need to add front matter.
-->
> Liquid 필터 `downcase` 의 결과를 보려면, Front matter을 추가해야 합니다.

<!--
Jekyll provides a number of useful Liquid additions to help you build your site:
-->

Jekyll 은 유용한 Liquid 기능 몇 가지를 추가로 제공하여 사이트 빌드를 도와줍니다
상세 설명을 보기위해 아래의 링크를 방문하세요 :

<!--
* [Filters](/docs/liquid/filters/)
* [Tags](/docs/liquid/tags/)
-->
* [태그](/docs/Jekyll/Jekyll Home/Jekyll_docs/tags/)
* [필터](/docs/Jekyll/Jekyll Home/Jekyll_docs/filters/)



