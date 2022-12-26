---
layout: default        # site layout 지정
title: Front Matter    # 
nav_order: 3
parent: Jekyll Home
grand_parent: Jekyll
my_number: 5
---

# Front matter
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

Jekyll 은 [YAML](https://yaml.org/) Front matter 블록을 가진 모든 파일( post, page )을
특별한 파일로 인식하여 처리합니다. Front matter은 반드시 파일의 맨 첫 부분에
위치해야 하고 시작과 끝을 대시문자(`---`) 세 개로 감싸서 올바른 YAML 형식으로 작성해야
합니다.    

이 대시문자 사이에 `사전-정의 변수`(*layout, title, dev_order, parmalink* 등)를 사용할 수 있고, 심지어 `자신만의 고유 변수`를 정의하는 것도 가능합니다.   
해당 파일은 물론 해당 페이지 또는 포스트에 연결된 layout이나 include에서도 Liquid 태그를 사용하여 이 변수들에 접근할 수 있습니다.

가장 기본적인 형태 사용 예 :

```yaml
---
layout: post
title: Blogging Like a Hacker
---
```

## Front matter을 사용하세요

<!--
Let's change the `<title>` on your site to populate using front matter:
-->

1. 사이트의 `<title>` 을 바꿉니다            : Test12
1. `my_number`를 Liquid 를 사용하여 출력한다 : 125

{% raw %}
```liquid
---
layout: default          # 페이지의 화면에 나타나는 layout 지정
title: Test12            # title 지정 (파일명: test.html -> Test12.html로 인식됨)
nav_order: 3             # navigation order 지정
# parent: Just the docs  - navigation 관련 - parent      경로지정
# grand_parent: Jekyll   - navigation 관련 - grandparent 경로지정
my_number: 125           # 사용자 정의 변수
---
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    <h1>{{ "Hello World!" | downcase }}</h1>
    <h3>{{ page.my_number }}</h3>
  </body>
</html>
```
result: 

![그림1](/assets/images/picture1.png){: height="150% width="150%"}
<!-- ![그림1](/assets/images/picture1.png){: height="150% width="150%" title="그림1"} -->



<!--
Note that in order for Jekyll to process any liquid tags on your page,
you _must_ include front matter on it. The most minimal snippet of front matter
you can include is:
-->

{: .note }
> Jekyll이 당신의 페이지에서 `Liquid 태그`를 처리하도록 하려면, _반드시_
Front matter가 있어야 한다는 사실을 잊지마세요.    
가장 단순한 형태의 Front matter은 다음과 같습니다(**변수 선언이 전혀 없는 형태**):

```yaml
---
---
```
<br>

{: .important}
>    만약 <a href="/docs/Jekyll/Jekyll Home/Jekyll_docs/variables/">Liquid 태그와 변수</a>는 사용하고 싶은데
>    Front matter에는 넣을만한 내용이 하나도 없다면, 그냥 비워두세요!
>    삼중 대시 행 사이에 아무 내용이 없어도, Jekyll 은 해당 파일을
>    처리합니다.    
>    (CSS 나 RSS 피드같은 파일에 유용합니다!)

<br>

{: .warning}
> **UTF-8 문자 인코딩 주의사항**   
> 인코딩으로 UTF-8 을 사용중이라면, 절대로 파일에 `BOM` 헤더 문자가 있으면 안됩니다.    
> 그렇지 않으면 Jekyll 에 아주, 아주 안 좋은 일이 벌어집니다.   
> Jekyll 을 윈도우즈에서 사용 할 때에만 발생하는 문제입니다.




<!--
## Predefined Global Variables
-->
## 사전-정의 전역 변수

<!--
There are a number of predefined global variables that you can set in the
front matter of a page or post.
-->
페이지 또는 포스트의 Front matter에 사용할 수 있는 다양한 `사전-정의 전역 변수`가
있습니다.

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
<!--
      <th>Variable</th>
      <th>Description</th>
-->
      <th>변수</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>layout</code></p>
      </td>
      <td>
        <p>

<!--
          If set, this specifies the layout file to use. Use the layout file
          name without the file extension. Layout files must be placed in the
          <code>_layouts</code> directory.
-->
          사용할 레이아웃 파일을 지정한다.<br>    
          레이아웃 파일은 반드시 <code>_layouts</code>디렉토리에 존재해야 한다.  <br> 
          레이아웃 파일명에서 확장자를 제외한 나머지 부분만 입력한다. 

        </p>
        <ul>
           <li>
            파일에서의 설정이 front matter defaults 설정에 우선한다.

          </li>         
          <li>
            <code>null</code>,  <code>none</code>을 사용하면 레이아웃을 사용하지 않고 파일을 처리한다.  해당 파일이 포스트 혹은 문서이고 
            <a href="/docs/Jekyll/Jekyll Home/Jekyll_docs/front-matter-defaults/">Front matter defaults</a>에 레이아웃이 지정되어 있는 경우 Front matter 설정값이 적용된다.
            
          </li>

        </ul>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>permalink</code></p>
      </td>
      <td>
        <p>

<!--
          If you need your processed blog post URLs to be something other than
          the site-wide style (default <code>/year/month/day/title.html</code>), then you can set
          this variable and it will be used as the final URL.
-->
          생성된 블로그 포스트 URL 을 사이트 전역 스타일(기본설정:
          <code>/year/month/day/title.html</code>)이 아닌 다른 스타일로 만드려면, 이
          변수를 사용하여 최종 URL로 사용한다.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>published</code></p>
      </td>
      <td>
        <p>
<!--
          Set to false if you don’t want a specific post to show up when the
          site is generated.
-->
          사이트가 생성되었을 때 특정 포스트가 나타나지 않게 하려면 <code>false</code> 로
          설정한다.
        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

{: .note}
> <div class="note">
>  <h3>Unpublished로 마크된 포스트 렌더링하기</h3>
>  <p>
>    Unpublished로 마크된 포스트에 대한 미리보기는, <code>jekyll serve</code> 또는 <code>jekyll build</code> 를
>    <code>--unpublished</code> switch와 함께 실행합니다. 또한 Jekyll에는 블로그 포스트만을
>    위해 특별히 제작된 <a href="/docs/Jekyll/Jekyll Home/Jekyll_docs/drafts/">초안(draft)</a>
>    기능이 있어 좀 더 편리하게 사용할 수 있습니다.
>  </p>
> </div>

<!--
## Custom Variables
-->
## 사용자-정의 변수

<!--
You can also set your own front matter variables you can access in Liquid. For
instance, if you set a variable called `food`, you can use that in your page:
-->
자신만의 Front matter 변수를 설정하여 Liquid에서 사용할 수도 있습니다. 예를
들어, `food` 라는 변수를 설정했다면, 이렇게 페이지에서 사용할 수 있습니다:

{% raw %}
```liquid
---
food: Pizza
---

<h1>{{ page.food }}</h1>
```
{% endraw %}

<!--
## Predefined Variables for Posts
-->
## 사전-정의 변수(post용)

<!--
These are available out-of-the-box to be used in the front matter for a post.
-->
다음은 포스트에서 사용할 수 있는 특별한 Front matter 변수들입니다.

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
<!--
      <th>Variable</th>
      <th>Description</th>
-->
      <th>변수</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p><code>date</code></p>
      </td>
      <td>
        <p>
<!--
          A date here overrides the date from the name of the post. This can be
          used to ensure correct sorting of posts. A date is specified in the
          format <code>YYYY-MM-DD HH:MM:SS +/-TTTT</code>; hours, minutes, seconds, and timezone offset
          are optional.
-->
          여기에 지정한 날짜가 포스트 이름에 있는 날짜보다 더 우선순위가 높다.<br>
          포스트를 올바르게 정렬하기 위해 사용할 수 있는 기능이다. <br> 날짜 형식은
          <code>YYYY-MM-DD HH:MM:SS +/-TTTT</code> 이다; 시간, 분, 초와 타임존
          오프셋은 선택사항이다.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>category</code></p>
        <p><code>categories</code></p>
      </td>
      <td>
        <p>

<!--
          Instead of placing posts inside of folders, you can specify one or
          more categories that the post belongs to. When the site is generated
          the post will act as though it had been set with these categories
          normally. Categories (plural key) can be specified as a <a
          href="https://en.wikipedia.org/wiki/YAML#Basic_components">YAML list</a> or a
          space-separated string.
-->
          포스트를 폴더 안에 넣는 대신, 포스트에 하나 또는
          여러 개의 카테고리를 지정할 수도 있다. <br> 사이트가 생성되면 post은 정상적으로 이러한 카테고리로 설정된 것처럼 작동합니다. 카테고리들(복수형)은 <a
          href="https://en.wikipedia.org/wiki/YAML#Basic_components">YAML list</a> 또는
          space-separated string( )로 정의한다.

        </p>
      </td>
    </tr>
    <tr>
      <td>
        <p><code>tags</code></p>
      </td>
      <td>
        <p>

<!--
          Similar to categories, one or multiple tags can be added to a post.
          Also like categories, tags can be specified as a <a
          href="https://en.wikipedia.org/wiki/YAML#Basic_components">YAML list</a> or a
          space-separated string.
-->
          카테고리와 비슷하게, 하나 또는 여러 개의 태그를 포스트에 추가할 수 있다.<br>
          또한 카테고리처럼, 태그는 <a
          href="https://en.wikipedia.org/wiki/YAML#Basic_components">YAML list</a> 또는
          space-separated string( )로 정의한다.

        </p>
      </td>
    </tr>
  </tbody>
</table>
</div>

{: .note}
>  <h3>같은 일을 반복하지 마세요</h3>
>   자주 사용하는 Front matter 변수를 계속 반복해서 입력하고 싶지 않으면, 해당 변수에
    대해 <a href="/docs/Jekyll/Jekyll Home/Jekyll_docs/front-matter-defaults/">디폴트 값</a>을     정의하고, 필요한 곳에서만 다른 값으로 덮어쓰세요. 사전-정의 변수와
    사용자-정의 변수 모두 이 방법을 적용할 수 있습니다.




