---
layout: default
title: structure
parent: Jekyll Home
grand_parent: Jekyll
---

# structure
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
<!--
A basic Jekyll site usually looks something like this:
-->
가장 기본적인 Jekyll 사이트는 보통 이렇게 생겼습니다:

<!--
```
.
├── _config.yml
├── _data
│   └── members.yml
├── _drafts
│   ├── begin-with-the-crazy-ideas.md
│   └── on-simplicity-in-technology.md
├── _includes
│   ├── footer.html
│   └── header.html
├── _layouts
│   ├── default.html
│   └── post.html
├── _posts
│   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
│   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
│   ├── _base.scss
│   └── _layout.scss
├── _site
├── .jekyll-metadata
└── index.html # can also be an 'index.md' with valid front matter
```
-->
```
.
├── _config.yml
├── _data
│   └── members.yml
├── _drafts
│   ├── begin-with-the-crazy-ideas.md
│   └── on-simplicity-in-technology.md
├── _includes
│   ├── footer.html
│   └── header.html
├── _layouts
│   ├── default.html
│   └── post.html
├── _posts
│   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
│   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
│   ├── _base.scss
│   └── _layout.scss
├── _site
├── .jekyll-metadata
└── index.html # 올바른 머리말을 가진 'index.md' 도 가능
```

{: .note}
>   <h3>루비 젬 기반 테마를 사용하는 Jekyll 사이트의 디렉토리 구조</h3>  
> 버전 {% include docs_version_badge.html version="3.2"%} 부터, <code>jekyll new</code> 명령으로 생성된 Jekyll 프로젝트는 <a href="/docs/Jekyll/Jekyll Home/themes/">루비 젬 기반 테마</a>를 사용하여 사이트의 외관을 구성합니다. 이로 인해, 테마 루비 젬에 기본적으로 포함된 경량 디렉토리 구조: <code>_layouts</code>, <code>_includes</code>, <code>_sass</code> 를 갖게 됩니다.
현재의 기본 테마는 <a href="https://github.com/jekyll/minima">minima</a> 이며, <code>bundle show minima</code> 명령으로 Minima 테마의 파일들이 어디에 저장되어 있는지 볼 수 있습니다.


<!--
An overview of what each of these does:
-->
각 파일과 디렉토리가 하는 일의 개요는 다음과 같습니다:

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
<!--
      <th>File / Directory</th>
      <th>Description</th>
-->
      <th>파일 / 디렉토리</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>_config.yml</code>
      </td>
      <td>
        
<!--
          Stores <a href="/docs/configuration/">configuration</a> data. Many of
          these options can be specified from the command line executable but
          it’s easier to specify them here so you don’t have to remember them.
-->
          <a href="/docs/Jekyll/Jekyll Home/Jekyll_configuration/">환경설정</a> 정보를 보관한다. 명령어를
          실행할 때 여러가지 옵션들을 추가할 수도 있지만, 그렇게 따로 외우는
          것보다 이 파일에 정의해두는게 더 편리하다.
        
      </td>
    </tr>
    <tr>
      <td>
        <code>_drafts</code>
      </td>
      <td>
        
<!--
          Drafts are unpublished posts. The format of these files is without a
          date: <code>title.MARKUP</code>. Learn how to <a href="/docs/posts/#drafts">
          work with drafts</a>.
-->
          초안이란 아직 게시하지 않은 포스트를 말한다. <br>파일명 형식에 날짜가
          없다: <code>title.MARKUP</code>. 사용 방법은 <a href="/docs/Jekyll/Jekyll Home/Jekyll_docs/drafts/">
          초안 활용하기</a>를 참고하라.
        
      </td>
    </tr>
    <tr>
      <td>
        <code>_includes</code>
      </td>
      <td>
        
<!--
          These are the partials that can be mixed and matched by your layouts
          and posts to facilitate reuse. The liquid tag
          <code>{% raw %}{% include file.ext %}{% endraw %}</code>
          can be used to include the partial in
          <code>_includes/file.ext</code>.
-->
          재사용하기 위한 파일을 담는 디렉토리로서, 필요에 따라 포스트나
          레이아웃에 쉽게 삽입할 수 있다.<br>
          <code>{% raw %}{% include file.ext %}{% endraw %}</code> 와 같이
          Liquid 태그를 사용하면 <code>_includes/file.ext</code> 파일에 담긴
          코드가 삽입된다.
        
      </td>
    </tr>
    <tr>
      <td>
        <code>_layouts</code>
      </td>
      <td>
        
<!--
          These are the templates that wrap posts. Layouts are chosen on a
          post-by-post basis in the
          <a href="/docs/front-matter/">front matter</a>,
          which is described in the next section. The liquid tag
          <code>{% raw %}{{ content }}{% endraw %}</code>
          is used to inject content into the web page.
-->
          포스트를 wrap할 때 사용하는 template이다. <br> 각 post 별로
          layout을 선택하는 기준은
          <a href="/docs/Jekyll/Jekyll Home/front matter/">front matter</a>이다.<br>
          <code>{% raw %}{{ content }}{% endraw %}</code> 와 같이 Liquid 태그를
          사용하면 페이지에 컨텐츠가 주입된다.
        
      </td>
    </tr>
    <tr>
      <td>
        <code>_posts</code>
      </td>
      <td>
        
<!--
          Your dynamic content, so to speak. The naming convention of these
          files is important, and must follow the format:
          <code>YEAR-MONTH-DAY-title.MARKUP</code>.
          The <a href="/docs/permalinks/">permalinks</a> can be customized for
          each post, but the date and markup language are determined solely by
          the file name.
-->
          한마디로 말하면, 당신의 contents이다. 중요한 것은 파일들의 명명규칙인데,
          반드시 이 형식을 따라야 한다:
          <code>YEAR-MONTH-DAY-title.MARKUP</code>.<br>
          <a href="/docs/Jekyll/Jekyll Home/Jekyll_docs/permalink/">permalink</a>는 포스트 별로 각각 정의할 수
          있지만, 날짜와 마크업 언어 종류는 오로지 파일명에 의해
          결정된다.
        
      </td>
    </tr>
    <tr>
      <td>
        <code>_data</code>
      </td>
      <td>
        
<!--
          Well-formatted site data should be placed here. The Jekyll engine
          will autoload all data files (using either the <code>.yml</code>,
          <code>.yaml</code>, <code>.json</code>, <code>.csv</code> or
          <code>.tsv</code> formats and extensions) in this directory,
          and they will be accessible via `site.data`. If there's a file
          <code>members.yml</code> under the directory, then you can access
          contents of the file through <code>site.data.members</code>.
-->
          사이트에 사용할 데이터를 적절한 포맷으로 정리하여 보관하는 디렉토리.<br>
          Jekyll 엔진은 이 디렉토리에 있는 (확장자와 포맷이 <code>.yml</code>
          또는 <code>.yaml</code>, <code>.json</code>, <code>.csv</code>,
          <code>.tsv</code> 인) 모든 데이터 파일을 자동으로 읽어들여
          <code>site.data</code> 로 사용할 수 있도록 만든다. <br> 만약 이 디렉토리에
          <code>members.yml</code> 라는 파일이 있다면,
          <code>site.data.members</code> 라고 입력하여 그 컨텐츠를 사용할 수 있다.
        
      </td>
    </tr>
    <tr>
      <td>
        <code>_sass</code>
      </td>
      <td>
        
<!--
          These are sass partials that can be imported into your <code>main.scss</code>
          which will then be processed into a single stylesheet
          <code>main.css</code> that defines the styles to be used by your site.
-->
          이것은 당신의 <code>main.scss</code> 에 임포트할 수 있는 Sass 조각들로서,
          하나의 스타일시트 파일 <code>main.css</code> 로 가공되어 당신의 사이트에서
          사용하는 스타일들을 정의한다.
        
      </td>
    </tr>
    <tr>
      <td>
        <code>_site</code>
      </td>
      <td>
        
<!--
          This is where the generated site will be placed (by default) once
          Jekyll is done transforming it. It’s probably a good idea to add this
          to your <code>.gitignore</code> file.
-->
          Jekyll 이 변환 작업을 마친 뒤 생성된 사이트가 저장되는 (디폴트)
          경로이다. 대부분의 경우, 이 경로를 <code>.gitignore</code> 에
          추가하는 것은 괜찮은 생각이다.
        
      </td>
    </tr>
    <tr>
      <td>
        <code>.jekyll-metadata</code>
      </td>
      <td>
        
<!--
          This helps Jekyll keep track of which files have not been modified
          since the site was last built, and which files will need to be
          regenerated on the next build. This file will not be included in the
          generated site. It’s probably a good idea to add this to your
          <code>.gitignore</code> file.
-->
          Jekyll 은 이 파일을 참고하여, 마지막으로 빌드한 이후에 한번도 수정되지
          않은 파일은 어떤 것인지, 다음 빌드 때 어떤 파일을 다시 생성해야 하는지
          판단할 수 있다. 생성된 사이트에 이 파일이 복사되지는 않는다. 대부분의
          경우, 이 파일을 <code>.gitignore</code> 에 추가하는 것은 괜찮은
          생각이다.
        
      </td>
    </tr>
    <tr>
      <td>
<!--
        <code>index.html</code> or <code>index.md</code> and other HTML,
        Markdown files
-->
        <code>index.html</code> 또는 <code>index.md</code> 및 다른 HTML,
        마크다운 파일
      </td>
      <td>
        
<!--
          Provided that the file has a <a href="/docs/front-matter/">front
          matter</a> section, it will be transformed by Jekyll. The same will
          happen for any <code>.html</code>, <code>.markdown</code>,
          <code>.md</code>, or <code>.textile</code> file in your site’s root
          directory or directories not listed above.
-->
          Jekyll 은 <a href="/docs/Jekyll/Jekyll Home/front matter/">머리말</a> 섹션을 가진 모든
          파일을 찾아 변환 작업을 수행한다. 위에서 언급하지 않은 다른 디렉토리나
          사이트의 루트 디렉토리에 있는 모든 <code>.html</code>,
          <code>.markdown</code>, <code>.md</code>, <code>.textile</code> 이
          여기에 해당한다.
        
      </td>
    </tr>
    <tr>
      <td>
<!--
        Other Files/Folders
-->
        다른 파일/폴더
      </td>
      <td>
        
<!--
          Every other directory and file except for those listed above—such as
          <code>css</code> and <code>images</code> folders,
          <code>favicon.ico</code> files, and so forth—will be copied verbatim
          to the generated site. There are plenty of <a href="/showcase/">sites
          already using Jekyll</a> if you’re curious to see how they’re laid
          out.
-->
          <code>css</code> 나 <code>images</code> 폴더, <code>favicon.ico</code>
          파일같이 앞서 언급하지 않은 다른 모든 디렉토리와 파일들은 있는 그대로
          생성된 사이트에 복사한다. <br>다른 사람들이 만든 사이트는 어떤식으로
          생겼는지 궁금하다면, <a href="https://jekyllrb.com/showcase/">Showcase Jekyll</a> 을 사용하는
          사이트들이 이미 많이 있으니 살펴보도록 한다.
        
      </td>
    </tr>
  </tbody>
</table>
</div>
