---
layout: default
title: layout
nav_order: 4
parent: Jekyll Home
grand_parent: Jekyll
---

# layouts
{: .no_toc }

### Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

<!--
Websites typically have more than one page and this website is no different.
-->
웹사이트는 보통 하나 이상의 페이지를 가지고 있으며 이 웹사이트 또한 마찬가지입니다.

<!--
Jekyll supports [Markdown](https://daringfireball.net/projects/markdown/syntax)
as well as HTML for pages. Markdown is a great choice for pages with a simple
content structure (just paragraphs, headings and images), as it's less verbose
than raw HTML. Let's try it out on the next page.
-->
Jekyll 은 HTML 뿐만 아니라 [마크다운](https://daringfireball.net/projects/markdown/syntax)도
지원합니다. 마크다운은 순수 HTML 보다 간략하여, 컨텐츠 구조가 단순한
페이지에 (예시, 문단, 제목, 이미지만 있는 문서) 탁월한 선택입니다.
<!--  다음 장에서 직접 해보기로 합니다. -->

<!--
Create `about.md` in the root.
-->
루트 디렉토리에 `about.md` 를 생성합니다.

<!--
For the structure you could copy `index.html` and modify it for the about page.
The problem with doing this is duplicate code. Let's say you wanted to add a
stylesheet to your site, you would have to go to each page and add it to the
`<head>`. It might not sound so bad for a two page site, imagine doing it
for 100 pages. Even simple changes will take a long time to make.
-->
구조를 통일하기 위해 `index.html` 을 복사하고 수정해서 about 페이지로 만들수도
있을 것입니다. 하지만 문제는 코드가 중복된다는 것입니다. 사이트에 스타일시트를
추가하는 상황을 가정해보면, 모든 페이지를 열어 `<head>` 에 스타일시트를
추가해야할 것입니다. 2 페이지 짜리 사이트에서는 문제될 것이 없지만, 100 페이지에
이 작업을 한다고 생각해보세요. 아주 작은 변경사항에도 시간이 많이 걸릴것입니다.

<!--
## Creating a layout
-->
## layout 생성하기

<!--
Using a layout is a much better choice. Layouts are templates that wrap around
your content. They live in a directory called `_layouts`.
-->
layout을 사용하는게 훨씬 더 나은 선택입니다. layout은 당신의 `컨텐츠를 포장하는
템플릿`입니다. `_layouts` 라는 디렉토리에 보관합니다.

<!--
Create your first layout at `_layouts/default.html` with the following content:
-->
다음과 같은 내용으로 `_layouts/default.html` 에 당신의 첫 번째 layout을 생성합니다:

{% raw %}
```liquid
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {{ content }}
  </body>
</html>
```
{% endraw %}

<!--
You'll notice this is almost identical to `index.html` except there's
no front matter and the content of the page is replaced with a `content`
variable. `content` is a special variable which has the value of the rendered
content of the page it's called on.
-->
내용이 `index.html` 과 거의 똑같다는 것을 눈치챌 수 있겠지만, Front matter가
없고 페이지의 컨텐츠 부분에 변수 `content` 가 사용되었다는 차이점이
있습니다. `content` 라는 이 특별한 변수는 자신이 호출된 페이지의 컨텐츠를
렌더링 한 내용을 담고 있습니다.

<!--
To have `index.html` use this layout, you can set a `layout` variable in front
matter. The layout wraps around the content of the page so all you need in
`index.html` is:
-->
`index.html` 에 이 layout을 사용하기 위해, `layout` 변수를 Front matter에
설정합니다.

{% raw %}
```liquid
---
layout: default
title: Home
---
<h1>{{ "Hello World!" | downcase }}</h1>
```
{% endraw %}

<!--
After doing this, the output will be exactly the same as before. Note that you
can access the `page` front matter from the layout. In this case `title` is
set in the index page's front matter but is output in the layout.
-->
이렇게 하면, 출력 결과는 이전과 완벽하게 동일할 것입니다. 기억할 것은
layout으로부터 페이지(`page`)의 Front matter에 접근한다는 것입니다. 위 예시에서, `title` 은
인덱스 페이지의 Front matter에 설정되었지만 layout에서 출력되었습니다.

<!--
## About page
-->
## 페이지에 관하여

<!--
Back to the about page, instead of copying from `index.html`, you can use the
layout.
-->
about 페이지로 돌아와서, `index.html` 을 복사하는 대신 layout을 사용할 수
있습니다.

<!--
Add the following to `about.md`:
-->
다음 내용을 `about.md` 에 추가합니다:

```markdown
---
layout: default
title: About
---
# About page

This page tells you a little bit about me.
```

<!--
Open <a href="http://localhost:4000/about.html" target="_blank" data-proofer-ignore>http://localhost:4000/about.html</a>
in your browser and view your new page.
-->
브라우저에서 <a href="http://localhost:4000/about.html" target="_blank" data-proofer-ignore>http://localhost:4000/about.html</a>
를 열어 새 페이지를 확인합니다.

<!--
Congratulations, you now have a two page website! But how do you
navigate from one page to another? Keep reading to find out.
-->
<!-- 축하합니다. 이제 두 페이지짜리 웹사이트가 생겼네요! 그런데
페이지간의 이동은 어떻게 하죠? 계속해서 알아봅시다. -->

# layouts 상세

<!--
Layouts are templates that wrap around your content. They allow you to have the
source code for your template in one place so you don't have to repeat things
like your navigation and footer on every page.
-->
layout은 컨텐츠를 포장하는 템플릿입니다. 템플릿을 위한 코드를 한 곳에 보관할
수 있게 해주기 때문에 모든 페이지에 네비게이션이나 푸터를 반복해서 입력할 필요가
없습니다.

<!--
Layouts live in the `_layouts` directory. The convention is to have a base
template called `default.html` and have other layouts [inherit](#inheritance)
from this as needed.
-->
layout은 `_layouts` 디렉토리에 위치합니다. 관례적으로 `default.html` 라는
이름의 기본 템플릿을 가지고 필요에 따라 [상속](#inheritance)해서 다른 layout을
만듭니다.

{: .note}
> <div class="note">
> <!--
>   <h5>Layouts Directory</h5>
> -->
>   <h5>layout 디렉토리</h5>
>   <p>
> <!--
>     Jekyll looks for the <code>_layouts</code> directory either at the root of
>     your site's <code>source</code> or at the root of your theme.
> -->
>     Jekyll 은 사이트 <code>source</code> 의 루트 또는 테마의 루트에서
>     <code>_layouts</code> 디렉토리를 찾습니다.
>   </p>
>   <p>
> 
> <!--
>     While you can configure the directory name in which your layouts can reside by
>     setting the <code>layouts_dir</code> key in your config file, the directory
>     itself should be located at the root of your site's <code>source</code> directory.
> -->
>     환경설정 파일에 <code>layouts_dir</code> 키를 설정해서 layout이 위치하는
>     디렉토리의 이름을 변경할 수 있지만, 해당 디렉토리는 반드시 사이트의
>     <code>source</code> 디렉토리에 위치해야만 합니다.
>   </p>
> </div>

<!--
## Usage
-->
## 사용법

<!--
The first step is to put the template source code in `default.html`. `content`
is a special variable, the value is the rendered content of the post or page
being wrapped.
-->
첫 단계는 `default.html` 에 템플릿 소스코드를 입력하는 것입니다. `content` 라는
특별한 변수가 있는데, 그 값은 포스트나 페이지의 렌더링 된
컨텐츠입니다.

{% raw %}
```liquid
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
    <link rel="stylesheet" href="/css/style.css">
  </head>
  <body>
    <nav>
      <a href="/">Home</a>
      <a href="/blog/">Blog</a>
    </nav>
    <h1>{{ page.title }}</h1>
    <section>
      {{ content }}
    </section>
    <footer>
      &copy; to me
    </footer>
  </body>
</html>
```
{% endraw %}

<!--
You have full access to the front matter of the origin. In the
example above, `page.title` comes from the page front matter.
-->
당신은 front matter에 대해 완전한 접근권한을 가지고 있습니다. 위
예제에서, `page.title` 은 페이지의 front matter로부터 비롯된 것입니다.

<!--
Next you need to specify what layout you're using in your page's front matter.
You can also use
[front matter defaults](/docs/configuration/front-matter-defaults/) to save you
from having to set this on every page.
-->
그 다음 할 일은 어떤 layout을 사용할 것인지 페이지의 front matter에 명시하는 것입니다.
그리고 [front matter defaults](/docs/Jekyll/Jekyll Home/Jekyll_docs/front-matter-defaults/)을 사용하면
모든 페이지에 같은 내용을 입력하지 않아도 됩니다.

```markdown
---
title: My First Page
layout: default
---

This is the content of my page
```

<!--
The rendered output of this page is:
-->
이 페이지의 렌더링된 결과물입니다:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>My First Page</title>
    <link rel="stylesheet" href="/css/style.css">
  </head>
  <body>
    <nav>
      <a href="/">Home</a>
      <a href="/blog/">Blog</a>
    </nav>
    <h1>My First Page</h1>
    <section>
      This is the content of my page
    </section>
    <footer>
      &copy; to me
    </footer>
  </body>
</html>
```

<!--
## Inheritance
-->
## 상속 {#inheritance}

<!--
Layout inheritance is useful when you want to add something to an existing
layout for a portion of documents on your site. A common example of this is
blog posts, you might want a post to display the date and author but otherwise
be identical to your base layout.
-->
layout 상속은 이미 존재하는 layout에 무언가 추가해서 사이트의 일부 문서에만
적용하고자 할 때 유용합니다. 이에 대한 간단한 예시로 블로그 포스트를 들 수
있는데, 포스트에는 날짜와 작성자를 표시하지만 나머지는 기본 layout과 똑같이
보이게 하는 것입니다.

<!--
To achieve this you need to create another layout which specifies your original
layout in front matter. For example this layout will live at
`_layouts/post.html`:
-->
이를 위해서는 새 layout을 만들어 그 front matter에 원래의 layout을 지정해야
합니다. 다음은 `_layouts/post.html` 라는 이름의 layout
예시입니다:

{% raw %}
```liquid
---
layout: default
---
<p>{{ page.date }} - Written by {{ page.author }}</p>

{{ content }}
```
{% endraw %}

<!--
Now posts can use this layout while the rest of the pages use the default.
-->
이제 포스트에는 이 layout을 사용하고 다른 페이지들에는 기본 layout을 사용합니다.

<!--
## Variables
-->
## 변수

<!--
You can set front matter in layouts, the only difference is when you're
using in Liquid, you need to use the `layout` variable instead of `page`. For
example:
-->
layout에도 front matter을 설정할 수 있는데, 유일한 차이점은 Liquid 를
사용할 때, `page` 대신 `layout` 을 사용해야 한다는 것입니다. 예를
들면 다음과 같습니다:

{% raw %}
```liquid
---
city: San Francisco
---
<p>{{ layout.city }}</p>

{{ content }}
```
{% endraw %}

