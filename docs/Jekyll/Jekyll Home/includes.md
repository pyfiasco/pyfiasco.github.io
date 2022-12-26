---
layout: default
title: includes
nav_order: 5
parent: Jekyll Home
grand_parent: Jekyll
---

# includes
{: .no_toc }

### Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Include 태그
<!--
The site is coming together; however, there's no way to navigate between
pages. Let's fix that.
-->
<!--
Navigation should be on every page so adding it to your layout is the correct
place to do this. Instead of adding it directly to the layout, let's use this
as an opportunity to learn about includes.
-->
네비게이션은 모든 페이지에 있어야 하므로 레이아웃에 추가하는 것이 올바른
방법입니다.    
레이아웃에 직접 추가하는 대신, 이 기회를 이용해 include에 대하여
배워보도록 합니다.

<!--
## Include tag
-->



<!--
The `include` tag allows you to include content from another file stored
in an `_includes` folder. Includes are useful for having a single source for
source code that repeats around the site or for improving the readability.
-->
`include` 태그를 사용하면 **_includes** 폴더에 저장된 include의 내용을
포함시킬 수 있습니다.    
Include은 사이트 여러곳에 반복되는 코드를 한 곳에서
관리하거나 소스코드의 가독성을 향상시키기 때문에 유용합니다.

<!--
Navigation source code can get complex so sometimes it's nice to move it into an
include.
-->
네비게이션을 구현하는 소스코드는 복잡한 경우가 많아 include로 보관하는 것이
좋습니다.

<!--
## Include usage
-->
## include 사용법

<!--
Create a file for the navigation at `_includes/navigation.html` with the
following content:
-->
네비게이션을 위한 파일을 `_includes/navigation.html` 에 생성하고 다음 내용을
저장합니다:

```
<nav>
  <a href="/">Home</a>
  <a href="/about.html">About</a>
</nav>
```

<!--
Try using the include tag to add the navigation to `_layouts/default.html`:
-->
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

<!--
Open <a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a>
in your browser and try switching between the pages.
-->
브라우저에서 <a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a>
를 열어 페이지 사이를 이동해봅니다.

<!--
## Current page highlighting
-->
## 현재 페이지 표시하기

<!--
Let's take this a step further and highlight the current page in the navigation.
-->
좀 더 깊게 파고들어서 네비게이션에 현재 페이지를 표시하는 방법을 알아봅시다.

<!--
`_includes/navigation.html` needs to know the URL of the page it's inserted into
so it can add styling. Jekyll has useful [variables](/docs/variables/) available
one of which is `page.url`.
-->
스타일을 추가하려면 `_includes/navigation.html` 은 자신이 삽입된 페이지의 URL 을
알 필요가 있습니다. Jekyll 에서 사용할 수 있는 유용한 [변수들]({% link docs/Jekyll/Jekyll Home/Jekyll_docs/variables.md %})
중 `page.url` 이라는 변수가 있습니다.

<!--
Using `page.url` you can check if each link is the current page and color it red
if true:
-->
`page.url` 을 사용해서 각 링크가 현재 페이지인지 확인하고 만약 그렇다면 빨간색으로
표시합니다:

{% raw %}
```liquid
<nav>
  <a href="/" {% if page.url == "/" %}style="color: red;"{% endif %}>
    Home
  </a>
  <a href="/about.html" {% if page.url == "/about.html" %}style="color: red;"{% endif %}>
    About
  </a>
</nav>
```
{% endraw %}

<!--
Take a look at <a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a>
and see your red link for the current page.
-->
브라우저에서 <a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a>
을 열어 현재 페이지 링크가 빨간색인지 확인합니다.

<!--
There's still a lot of repetition here if you wanted to add a new item to the
navigation or change the highlight color. In the next step we'll address this.
-->
네비게이션에 새 페이지를 추가하거나 색을 변경하고자 하는 경우 여전히 중복된
코드가 많이 발생합니다. 
<!-- 다음 단계에서 이에 대해 다뤄보겠습니다. -->


# include 상세

<!--
The `include` tag allows you to include the content from another file stored in the `_includes` folder:
-->
`include` 태그를 사용하면 `_includes` 폴더에 저장된 다른 파일의 내용을 포함시킬 수 있습니다:

{% raw %}
```liquid
{% include footer.html %}
```
{% endraw %}

<!--
Jekyll will look for the referenced file (in this case, `footer.html`) in the `_includes` directory at the root of your source directory and insert its contents.
-->
Jekyll 은 Site Source 최상위 디렉토리의 `_includes` 디렉토리에서 참조된 파일 (여기서는, `footer.html`) 을 찾아 그 내용을 삽입합니다.

<!--
### Including files relative to another file
-->
### 상대경로로 파일 삽입하기

<!--
You can choose to include file fragments relative to the current file by using the `include_relative` tag:
-->
`include_relative` 태그를 사용하면 현재 파일로부터의 상대경로로 삽입할 include을 선택할 수 있습니다:

{% raw %}
```liquid
{% include_relative somedir/footer.html %}
```
{% endraw %}

<!--
You won't need to place your included content within the `_includes` directory. Instead,
the inclusion is specifically relative to the file where the tag is being used. For example,
if `_posts/2014-09-03-my-file.markdown` uses the `include_relative` tag, the included file
must be within the `_posts` directory or one of its subdirectories.
-->
included content를 `_includes` 디렉토리에 보관할 필요가 없습니다. 그 대신, 태그가 사용된 파일이
있는 위치로부터의 상대경로로 삽입할 파일을 선택합니다. 예를 들어, `include_relative` 태그를
사용한 위치가 `_posts/2014-09-03-my-file.markdown` 이라면, include은 `_posts` 디렉토리
혹은 그 하위 디렉토리 안에 있어야 합니다.

<!--
Note that you cannot use the `../` syntax to specify an include location that refers to a higher-level directory.
-->

{: .note}
>include의 위치를 지정할 때 상위 디렉토리를 가리키는 `../` 문법은 사용할 수 없다는 점을 알아두세요.

<!--
All the other capabilities of the `include` tag are available to the `include_relative` tag,
such as variables.
-->
예를 들면,  `include` 태그의 다른 모든 기능은  `include_relative` 태그에서도
사용할 수 있습니다(변수 처럼).

<!--
### Using variables names for the include file
-->
### include에 대해 변수 사용하기

<!--
The name of the file you want to embed can be specified as a variable instead of an actual file name. For example, suppose you defined a variable in your page's front matter like this:
-->
끼워넣고자 하는 파일은 실제 파일이름이 아닌 변수를 사용해서 지정할 수도 있습니다. 예를들어 페이지의 front matter에 다음과 같은 변수를 정의했다고 가정해봅시다:

```yaml
---
title: My page
my_variable: footer_company_a.html
---
```

<!--
You could then reference that variable in your include:
-->
그 다음엔 태그에 이 변수를 사용할 수 있습니다:

{% raw %}
```liquid
{% if page.my_variable %}
  {% include {{ page.my_variable }} %}
{% endif %}
```
{% endraw %}

<!--
In this example, the include would insert the file `footer_company_a.html` from the `_includes/footer_company_a.html` directory.
-->
이 예제에서는, `_includes` 디렉토리의 `footer_company_a.html` 파일이 삽입될 것입니다.

<!--
### Passing parameters to includes
-->
### include에 파라메터 사용하기

<!--
You can also pass parameters to an include. For example, suppose you have a file called `note.html` in your `_includes` folder that contains this formatting:
-->
태그에 파라메터도 사용할 수 있습니다. 예를 들어, `_includes` 폴더에 다음과 같은 내용을 가진 `note.html` 파일을 가지고 있다고 가정해봅시다:

{% raw %}
```liquid
<div markdown="span" class="alert alert-info" role="alert">
<i class="fa fa-info-circle"></i> <b>Note:</b>
{{ include.content }}
</div>
```
{% endraw %}

<!--
The {% raw %}`{{ include.content }}`{% endraw %} is a parameter that gets populated when you call the include and specify a value for that parameter, like this:
-->
`{% raw %}{{ include.content }}{% endraw %}` 는 파라메터로서 다음과 같이 `include` 태그를 파라메터 대한 값과 함께 호출하면 그 값이 입력됩니다.

{% raw %}
```liquid
{% include note.html content="This is my sample note." %}
```
{% endraw %}

<!--
The value of `content` (which is `This is my sample note`) will be inserted into the {% raw %}`{{ include.content }}`{% endraw %} parameter.
-->
`content` 의 값 (여기서는 `This is my sample note`) 이 {% raw %}`{{ include.content }}`{% endraw %} 파라메터에 삽입될 것입니다.

<!--
Passing parameters to includes is especially helpful when you want to hide away complex formatting from your Markdown content.
-->
이렇게 `include` 태그에 파라메터를 사용하는 기법은 특히 마크다운에서 복잡한 형태의 내용을 숨기는데에 도움이 됩니다.

<!--
For example, suppose you have a special image syntax with complex formatting, and you don't want your authors to remember the complex formatting. As a result, you decide to simplify the formatting by using an include with parameters. Here's an example of the special image syntax you might want to populate with an include:
-->
예를 들어, 당신이 사용중인 이미지 삽입 코드가 다음과 같이 복잡한 형태이고, 포스트 작성자들이 이 코드를 외울 필요가 없게 만들고 싶다고 가정해봅시다. 결과적으로, 당신은 `include` 태그와 파라메터를 사용해서 코드를 단순하게 만들 것입니다. 여기 `include` 태그와 파라메터를 활용하기 좋은 이미지 삽입 코드 예제가 있습니다:

```html
<figure>
   <a href="http://jekyllrb.com">
   <img src="logo.png" style="max-width: 200px;"
      alt="Jekyll logo" />
   </a>
   <figcaption>This is the Jekyll logo</figcaption>
</figure>
```

<!--
You could templatize this content in your include and make each value available as a parameter, like this:
-->
이 코드는 각각의 값들에 파라메터를 사용하는 include로 템플릿처럼 만들 수 있습니다, 이렇게요:

{% raw %}
```liquid
<figure>
   <a href="{{ include.url }}">
   <img src="{{ include.file }}" style="max-width: {{ include.max-width }};"
      alt="{{ include.alt }}"/>
   </a>
   <figcaption>{{ include.caption }}</figcaption>
</figure>
```
{% endraw %}

<!--
This include contains 5 parameters:
-->
여기에는 5 개의 파라메터가 있습니다:

* `url`
* `max-width`
* `file`
* `alt`
* `caption`

<!--
Here's an example that passes all the parameters to this include (the include file is named `image.html`):
-->
파라메터와 함께 이 include을 사용하는 예제가 여기 있습니다 (include의 이름은 `image.html` 입니다):

{% raw %}
```liquid
{% include image.html url="http://jekyllrb.com"
max-width="200px" file="logo.png" alt="Jekyll logo"
caption="This is the Jekyll logo." %}
```
{% endraw %}

<!--
The result is the original HTML code shown earlier.
-->
그 결과는 위의 HTML 코드와 동일합니다.

<!--
To safeguard situations where users don't supply a value for the parameter, you can use [Liquid's default filter](https://shopify.github.io/liquid/filters/default/).
-->
사용자가 파라메터를 사용하지 않았을 때를 대비한 안전장치로서, [Liquid 디폴트 필터](https://shopify.github.io/liquid/filters/default/)를 사용할 수 있습니다.

<!--
Overall, you can create includes that act as templates for a variety of uses &mdash; inserting audio or video clips, alerts, special formatting, and more. Note that you should avoid using too many includes, as this will slow down the build time of your site. For example, don't use includes every time you insert an image. (The above technique shows a use case for special images.)
-->
정리하자면, 템플릿같은 역할을 하는 include을 만들어 다양한 방식으로 사용할 수 있습니다 &mdash; 음성이나 영상, 경고문구, 특별한 코드 등의 삽입. include을 너무 많이 사용하는 것은, 사이트의 빌드 시간을 느리게 만드므로, 가급적 피해야 합니다. 예를 들어, 이미지를 삽입할 때마다 매번 include을 사용하는 것은 좋지 않습니다. (위의 예시는 특별취급해야하는 일부 이미지에 사용할만한 기법입니다.)

<!--
### Passing parameter variables to includes
-->
### include에 변수 파라메터 사용하기

<!--
Suppose the parameter you want to pass to the include is a variable rather than a string. For example, you might be using {% raw %}`{{ site.product_name }}`{% endraw %} to refer to every instance of your product rather than the actual hard-coded name. (In this case, your `_config.yml` file would have a key called `product_name` with a value of your product's name.)
-->
include의 파라메터에 문자열이 아닌 변수를 전달하려는 경우를 가정해봅시다. 예를 들어, 당신의 제품을 언급하는 모든 부분에 직접 제품이름을 입력하는 대신 {% raw %}`{{ site.product_name }}`{% endraw %} 을 사용할 수 있습니다. (이 경우, 당신의 `_config.yml` 파일에는 `product_name` 라는 키가 있고 그 값은 제품이름이어야 합니다.)

<!--
The string you pass to your include parameter can't contain curly braces. For example, you can't pass a parameter that contains this: {% raw %}`"The latest version of {{ site.product_name }} is now available."`{% endraw %}
-->
include 파라메터에는 중괄호를 사용할 수 없습니다. 예를 들어, 파라메터에는 다음과 같은 내용을 넣을 수 없습니다: {% raw %}`"The latest version of {{ site.product_name }} is now available."`{% endraw %}

<!--
If you want to include this variable in your parameter that you pass to an include, you need to store the entire parameter as a variable before passing it to the include. You can use `capture` tags to create the variable:
-->
include의 파라메터에 변수를 사용하려면, include을 사용하기 전에 먼저 파라메터를 변수로 저장해야 합니다. `capture` 태그를 사용해서 변수를 생성할 수 있습니다:

{% raw %}
```liquid
{% capture download_note %}
The latest version of {{ site.product_name }} is now available.
{% endcapture %}
```
{% endraw %}

<!--
Then pass this captured variable into the parameter for the include. Omit the quotation marks around the parameter content because it's no longer a string (it's a variable):
-->
이제 캡쳐한 변수를 include의 파라메터로 전달합니다. 따옴표는 쓰지 마세요. 이 파라메터는 더 이상 문자열이 아니니까요 (변수입니다):

{% raw %}
```liquid
{% include note.html content=download_note %}
```
{% endraw %}
