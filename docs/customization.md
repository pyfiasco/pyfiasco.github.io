---
layout: default
title: Customization
nav_order: 3
parent: Just the docs
grand_parent: Jekyll

---

# Customization
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Color schemes(색 구성표)   
<br>
`Just the docs` site는 light (default), dark의 두가지 색 구성표를 지원합니다.    
`_config.yml` 파일에서 ***color_scheme*** 매개변수를 설정하여 변경한다.

#### Example
{: .no_toc }

```yaml
# Color scheme supports "light" (default) and "dark"
color_scheme: dark
```

<button class="btn js-toggle-dark-mode">미리보기 [ dark color scheme ]</button>

<script>
const toggleDarkMode = document.querySelector('.js-toggle-dark-mode');

jtd.addEvent(toggleDarkMode, 'click', function(){
  if (jtd.getTheme() === 'dark') {
    jtd.setTheme('light');
    toggleDarkMode.textContent = 'Preview dark color scheme';
  } else {
    jtd.setTheme('dark');
    toggleDarkMode.textContent = 'Return to the light side';
  }
});
</script>


## Custom schemes( 사용자 지정 구성표)   

### Custom schemes 정의

사용자 지정 구성표를 추가할 수 있습니다. (색상, 글꼴, 간격 등을 변경 가능)   
> 사용자 정의 scheme 이름 : `foo`    
파일 경로               : ***_sass / color_schemes / foo.scss*** 파일 생성    

{: .note }
기본 색 구성표가 `light`이므로 사용자 지정 구성표는 묵시적으로 `light scheme` 에서 사용하는 변수 설정을 기반으로 합니다.    
   
   
사용자 지정 구성표가 `dark scheme` 를 기반으로 하도록 하려면 다음 명령으로 파일을 시작해야 합니다.

```scss
@import "./color_schemes/dark";
```   

   
동일한 방식으로 다른 사용자 지정 구성표를 기반으로 사용자 지정 구성표를 정의할 수 있습니다. 

사용 가능한 변수는 `_sass/support/_variables.scss` 파일에 나열되어 있습니다. ( [\_variables.scss](https://github.com/just-the-docs/just-the-docs/tree/main/_sass/support/_variables.scss) )

**예를 들어, `링크 색상`을 `자주색` 기본값에서 `파란색`으로 변경하려면 scheme 파일 내에 다음을 포함합니다.**


#### Example
{: .no_toc }

```scss
$link-color: $blue-000;
```

명심하라! 변수를 변경하는 것이 그것에 의존하는 다른 변수의 값을 자동으로 변경하지 않는다는 것이다.
예로 기본 link color (`$link-color`)은 `$purple-000`인데, 사용자 정의 색상 구성표에서 `$purple-000` 을 재정의하는 것이 그것을 매칭하기 위해 `$link-color` 를 자동으로 변경하지는 않는다. 대신 이전에 `cascaded values` 을 사용하는 각 변수는 `_variables.scss`에서 종속 규칙을 복사하여 수동으로 다시 구현해야 합니다(이 경우 `$link-color: $purple-000;`을 다시 작성).   

_Note:_ `_sass/support/variables.scss`에서 직접 변수를 편집하는 것은 권장되지 않으며 다른 종속성이 실패할 수 있습니다. 사용자 지정 구성표 파일을 사용하십시오.


### 사용자 지정 구성표 사용 

사용자 지정 구성표를 사용하려면 사이트의 `_config.yml` 파일에서 ***color_scheme*** 매개 변수만 설정하십시오 : 


```yaml
color_scheme: foo
```

### 전환 가능한 사용자 지정 구성표 

예를 들어 자바 스크립트를 통해 스키마를 동적으로 변경하려면 `assets/css/just-the-docs-foo.scss` 파일을 추가하십시오 

{% raw %}
    ---
    ---
    {% include css/just-the-docs.scss.liquid color_scheme="foo" %}
{% endraw %}


이를 통해 다음 `자바 스크립트`를 통해 구성표를 전환 할 수 있습니다.

```js
jtd.setTheme("foo")
```

버튼 toggle 사용 예 (추가)
```yml
<button class="btn js-toggle-dark-mode">Preview dark color scheme</button>

<script>
const toggleDarkMode = document.querySelector('.js-toggle-dark-mode');

jtd.addEvent(toggleDarkMode, 'click', function(){
  if (jtd.getTheme() === 'dark') {
    jtd.setTheme('light');
    toggleDarkMode.textContent = 'Preview dark color scheme';
  } else {
    jtd.setTheme('dark');
    toggleDarkMode.textContent = 'Return to the light side';
  }
});
</script>
```


## Override 및 완전한 사용자 정의 style

변수로 정의되지 않은 스타일의 경우 특정 `CSS class`를 수정할 수 있습니다. 또한 콘텐츠에 지정된 완전한 사용자 정의 CSS를 추가 할 수 있습니다. 이렇게 하려면 스타일을 `_sass/custom/custom.scss` 파일에 넣습니다. 이렇게 하면 모든 override를 단일 파일에 유지하고 업스트림 변경 내용을 계속 적용할 수 있습니다.    

예를 들어 페이지 인쇄를 위한 고유한 스타일을 추가하려면 다음 스타일을 추가할 수 있습니다.


#### Example
{: .no_toc }

```scss
// Print-only styles.
@media print {
  .side-bar,
  .page-header {
    display: none;
  }
  .main-content {
    max-width: auto;
    margin: 1em;
  }
}
```

## Override includes

제공하는 사용자 지정 [**Jekyll includes**](https://jekyllrb-ko.github.io/docs/includes/) 파일을 재정의하여 테마를 사용자 지정할 수 있습니다. 이렇게 하려면 `_includes` 디렉터리를 만들고 수정하려는 특정 파일의 복사본을 만듭니다. 이 파일의 내용은 테마 기본값을 재정의합니다. 이 프로세스에 대한 자세한 내용은 Jekyll 문서( [**Overriding theme defaults**](https://jekyllrb-ko.github.io/docs/themes/#테마-기본값-덮어쓰기))에서 확인할 수 있습니다.
 
Just the docs은  다음과 같은 사용자 지정 includes 파일을 제공합니다 :

### TOC Heading 사용자 정의

`_includes/toc_heading_custom.html`

페이지에 자식 페이지가 있고 `has_toc`가 `false`로 설정되지 않은 경우 이 콘텐츠는 그 페이지의 콘텐츠 뒤에 자식 페이지의 자동 생성 list 위에 heading으로 표시됩니다.

#### Example
{: .no_toc }

기본 TOC heading 을 “Contents” 으로 변경하려면 _includes/toc_heading_custom.html 를 만들고 다음을 추가합니다.

```html
<h2 class="text-delta">Contents</h2>
```

`text-delta` 클래스(옵션) 는 `heading` 을 **Contents**{:.text-delta} 로 표시합니다.


### Footer 사용자 정의

`_includes/footer_custom.html`

이 콘텐츠는 모든 페이지의 기본 콘텐츠 하단에 표시됩니다. 이 포함에 대한 자세한 내용은 [Configuration - Footer content]({{ site.baseurl }}{% link docs/configuration.md %}#footer-content) 에서 찾을 수 있습니다.


### Head 와 Favicon 사용자 지정

`_includes/head_custom.html`

이 파일에 추가된 모든 HTML은 `<head>` 태그 전에 삽입됩니다.. 여기에는 추가 `<meta`>, `<link>`, `<script>` tags 포함 가능.


기본적으로 이 파일의 내용은 다음과 같습니다.
```html
<link rel="shortcut icon" href="/just-the-docs/favicon.ico" type="image/x-icon">
```
or

```html
<link rel="shortcut icon" type="image/png" href="{{site.baseurl}}/path/to/your/favicon.png">
```

#### EXAMPLE: CUSTOM FAVICON
{: .no_toc }

사용자 지정 favicon 을 추가하려면 `_includes/head_custom.html` 를 만들고 다음을 추가합니다.

```html
<link rel="shortcut icon" href="/just-the-docs/favicon.ico" type="image/x-icon">
```
favicon 이 필요하지 않으면 빈 `_includes/head_custom.html` 이 필요합니다.


### Header 사용자 지정

`_includes/header_custom.html`

이 파일에 추가된 콘텐츠는 모든 페이지의 기본 콘텐츠 맨 위에 나타납니다. 사이트 검색과 보조 링크가 활성화된 경우 사이에 나타난다. `search_enabled`가 `false`로 설정되고 `aux_links` 제거되면 `header_custom.html`의 내용이 모든 페이지의 맨 위 공간을 차지합니다.


### Nav Footer 사용자 지정

`_includes/nav_footer_custom.html`

이 파일에 추가된 모든 콘텐츠는 사이트 탐색 아래 페이지의 왼쪽 하단에 표시됩니다. 기본적으로 Just the Docs에 대한 저작자 표시가 표시됩니다.`This site uses Just the Docs, a documentation theme for Jekyll.`


### Search Placeholder 사용자 지정

`_includes/search_placeholder_custom.html`

이 파일에 추가된 콘텐츠는 HTML과 선행/후행 공백을 제거한 후 검색 표시줄(그리고 `aria-label`)의 기본 placeholder 텍스트를 대체합니다. 기본적으로 포함의 내용은 다음과 같습니다.

{% raw %}

```liquid
Search {{site.title}}
```

{% endraw %}


이 파일을 재정의하여 사용자 지정 placeholder 를 렌더링합니다. 일반적인 `use-case`는 `internationalization` 이다. 예를 들어


{% raw %}

```liquid
Chercher notre site
```

{% endraw %}

placeholder 텍스트를 "Chercher notre site"로 만듭니다. [Liquid code](https://jekyllrb-ko.github.io/docs/liquid/) ([Jekyll variables](https://jekyllrb-ko.github.io/docs/variables/) 포함)도 지원됩니다.