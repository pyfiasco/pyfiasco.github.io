---
layout: default
title: variables
parent: Jekyll_docs
grand_parent: Jekyll Home
---

# variables
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<!--
Jekyll traverses your site looking for files to process. Any files with
[front matter](/docs/front-matter/) are subject to processing. For each of these
files, Jekyll makes a variety of data available via the [Liquid](/docs/liquid/).
The following is a reference of the available data.
-->
Jekyll 은 작업이 필요한 파일을 찾아 사이트 내부를 이리저리 돌아다닙니다.    
작업 대상은 [Front matter](/docs/Jekyll/Jekyll Home/front matter/)을 가진 모든 파일입니다.    
Jekyll 은 [Liquid](/docs/Jekyll/Jekyll Home/liquid/)를 통해 각각의 작업 대상 파일마다 다양한 데이터를 생성합니다.
사용할 수 있는 데이터 목록은 다음과 같습니다.

<!--
## Global Variables
-->
## 전역 변수

{% include docs_variables_table.html scope=site.data.jekyll_variables.global %}

<!--
## Site Variables
-->
## 사이트 변수

{% include docs_variables_table.html scope=site.data.jekyll_variables.site %}

<!--
## Page Variables
-->
## 페이지 변수

{% include docs_variables_table.html scope=site.data.jekyll_variables.page %}


{: .note}
> <div class="note">
> <!--
>  <h5>ProTip™: Use Custom Front Matter</h5>
>-->
>  <h3 ><bold>ProTip™: 사용자정의 Front Matter를 사용하세요</bold></h3>
>  <p>
><!--
>    Any custom front matter that you specify will be available under
>    <code>page</code>. For example, if you specify <code>custom_css: true</code>
>    in a page’s front matter, that value will be available as <code>page.custom_css</code>.
>-->
>    모든 사용자정의 Front matter은 <code>page</code> 변수에서 사용할 수 있습니다.
>    예를 들어, 페이지 Front matter에 <code>custom_css: true</code> 를 설정한 경우,
>    <code>page.custom_css</code> 로 해당 값을 사용할 수 있습니다.
>  </p>
>  <p>
><!--
>    If you specify front matter in a layout, access that via <code>layout</code>.
>    For example, if you specify <code>class: full_page</code> in a layout’s front matter,
>    that value will be available as <code>layout.class</code> in the layout and its parents.
>-->
>    레이아웃에서 Front matter을 지정했다면, <code>layout</code> 을 통해 접근할 수 있습니다.
>    예를 들어, 레이아웃의 Front matter에 <code>class: full_page</code> 라고 설정했다면,
>    해당 레이아웃과 그 부모 레이아웃에서 <code>layout.class</code> 로 사용할 수 있습니다.
>  </p>
></div>

## Paginator

{% include docs_variables_table.html scope=site.data.jekyll_variables.paginator %}

{: .note}
> <h3>Paginator 변수 사용 위치</h3>
이 변수들은 오직 인덱스 파일에서만 사용할 수 있지만, <code>/blog/index.html</code> 같은
하위 디렉토리에 위치할 수 있다.

