---
layout: default
title: static-files
parent: Jekyll_docs
grand_parent: Jekyll Home
---

# static file
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## static file 의미
<!--
A static file is a file that does not contain any front matter. These
include images, PDFs, and other un-rendered content.
-->
static file은 front matter가 없는 파일을 뜻합니다.    
이미지나 PDF 들, 그 밖에
렌더링되지 않는 컨텐츠들이 여기에 속합니다.

<!--
They're accessible in Liquid via `site.static_files` and contain the
following metadata:
-->
이 파일들은 **site.static_files** 라는 `Liquid 태그`를 통해 접근할 수 있으며, 다음과
같은 메타데이터를 갖고 있습니다:

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
      <td><code>file.path</code></td>
      <td>

<!--
        The relative path to the file, e.g. <code>/assets/img/image.jpg</code>
-->
        파일에 대한 상대 경로. <br>예, <code>/assets/img/image.jpg</code>

      </td>
    </tr>
    <tr>
      <td><code>file.modified_time</code></td>
      <td>

<!--
        The `Time` the file was last modified, e.g. <code>2016-04-01 16:35:26 +0200</code>
-->
        파일이 마지막으로 수정된 `Time`. <br>예, <code>2016-04-01 16:35:26 +0200</code>

      </td>
    </tr>
    <tr>
      <td><code>file.name</code></td>
      <td>

<!--
        The string name of the file e.g. <code>image.jpg</code> for <code>image.jpg</code>
-->
        파일 이름. <br>예시, <code>image.jpg</code> 의 경우 <code>image.jpg</code>

      </td>
    </tr>
    <tr>
      <td><code>file.basename</code></td>
      <td>

<!--
        The string basename of the file e.g. <code>image</code> for <code>image.jpg</code>
-->
        확장자를 제외한 파일 이름. <br>예시, <code>image.jpg</code> 의 경우 <code>image</code>

      </td>
    </tr>
    <tr>
      <td><code>file.extname</code></td>
      <td>

<!--
        The extension name for the file, e.g.
        <code>.jpg</code> for <code>image.jpg</code>
-->
        파일의 확장자 이름. <br> 예시,
        <code>image.jpg</code> 의 경우 <code>.jpg</code>

      </td>
    </tr>
  </tbody>
</table>
</div>

<!--
Note that in the above table, `file` can be anything. It's an arbitrarily set variable used in your own logic (such as in a for loop). It isn't a global site or page variable.
-->
위의 표에서, 무엇이든 `file` 이 될 수 있습니다. 이는 (for 루프 같은) 당신의 로직에서 사용되는 변수를 임의로 설정합니다. 이는 글로벌 사이트 변수나 페이지 변수가 아닙니다.

<!--
## Add front matter to static files
-->
## static file에 front matter 넣기

<!--
Although you can't directly add front matter values to static files, you can set front matter values through the [defaults property](/docs/configuration/front-matter-defaults/) in your configuration file. When Jekyll builds the site, it will use the front matter values you set.
-->
static file에 front matter을 직접 넣을 수는 없지만, 환경설정 파일의 [디폴트 프로퍼티](/docs/Jekyll/Jekyll Home/Jekyll_docs/front-matter-defaults/)를 통해서 front matter 값들을 설정할 수 있습니다. Jekyll 은 사이트를 생성할 때, 당신이 설정한 front matter 값을 사용할 것입니다.

<!--
Here's an example:
-->
여기 예시가 있습니다:   
<!--
In your `_config.yml` file, add the following values to the `defaults` property:
-->
당신의 **_config.yml** 파일에, **defaults** property 값으로 다음 내용을 추가하세요:

```yaml
defaults:
  - scope:
      path: "assets/img"
    values:
      image: true
```

<!--
This assumes that your Jekyll site has a folder path of `assets/img` where  you have images (static files) stored. When Jekyll builds the site, it will treat each image as if it had the front matter value of `image: true`.
-->
이 설정은 당신의 Jekyll 사이트에 이미지 (static file) 들이 저장된 폴더가 `assets/img` 라는 경로에 있다고 가정합니다. Jekyll 은 사이트를 생성할 때, 이 경로의 이미지들이 `image: true` 라는 front matter 값을 가지고 있는 것처럼 취급합니다.

<!--
Suppose you want to list all your image assets as contained in `assets/img`. You could use this for loop to look in the `static_files` object and get all static files that have this front matter property:
-->
당신의 `assets/img` 에 들어있는 모든 이미지 자원을 나열하는 경우를 가정해봅시다. 이 for 루프를 사용하면 `static_files` 객체를 확인하여 이 front matter 프로퍼티를 가지고 있는 모든 static file을 얻을 수 있습니다:

{% raw %}
```liquid
{% assign image_files = site.static_files | where: "image", true %}
{% for myimage in image_files %}
  {{ myimage.path }}
{% endfor %}
```
{% endraw %}

<!--
When you build your site, the output will list the path to each file that meets this front matter condition.
-->
사이트를 생성할 때, 이 front matter 조건을 만족하는 모든 파일의 경로를 나열하게될 것입니다.
