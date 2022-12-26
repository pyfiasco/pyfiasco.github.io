---
layout: default
title: Navigation Structure
parent: Just the docs
grand_parent: Jekyll
---

# Navigation Structure
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }

1. TOC
{:toc}

</details>

---
## Main navigation(기본 탐색)

* Just the Docs 사이트의 기본 탐색은 큰 화면에서는 페이지 왼쪽에 있고 작은 화면에서는 상단(탭 형식으로)에 있습니다.  
* `title` 매개변수가 없는 페이지는 기본 탐색에서 자동으로 제외됩니다. 
* 기본적으로 모든 페이지는 `parent` 매개 변수가 정의되지 않는 한 기본 탐색에서 top level 페이지로 표시됩니다.     
* 기본 탐색은 다단계 메뉴 시스템(최대 `3 Level`)을 수용하도록 구성할 수 있습니다.     

---

## Ordering pages(페이지 순서 매기기)

페이지 순서를 지정하려면 페이지의 `YAML front matter`에서 `nav_order` 매개 변수를 사용할 수 있습니다.

#### Example
{: .no_toc }

```yaml
---
layout: default
title: Customization
nav_order: 4
---

```

매개 변수 값은 최상위 페이지 또는 부모가 같은 자식 페이지의 순서를 결정합니다. 부모 페이지가 다르면 동일 매개 변수가 존재할 수 있다. 

* 매개 변수 값은 숫자(정수, 부동 소수점), / , 문자열일 수 있습니다. 
* `nav_order` 매개 변수를 생략하면 기본적으로 `title`의 변수값이 사용됩니다. 
* 페이지 순서를 `title`과 독립적으로 만들려면 모든 페이지에 명시적 `nav_order` 매개 변수를 설정할 수 있습니다.
* 우선 순위는 숫자 > 문자열( 대문자 > 소문자 )  
> `nav_sort: case_insensitive` 추가하여 대/소문자 구분을 무시할 수 있습니다.

---

## Excluding pages(페이지 탐색 제외)
기본 탐색에 포함하지 않으려는 특정 페이지(예: 404 페이지)의 경우 해당 페이지의 `YAML front matter`에 `nav_exclude: true` 매개변수를 사용합니다.

#### Example
{: .no_toc }

```yaml
---
layout: default
title: 404
nav_exclude: true
---

```

`nav_exclude` 매개 변수는 하위 페이지의 자동 생성 목록에 영향을 주지 않습니다. 

---

## Pages with children(자식을 갖은 페이지)

때로는 많은 자식이 있는 페이지를 만들고 싶을 것입니다.   
첫째, 디렉토리명과 관련된 페이지를 함께 보관하는 것이 좋습니다. 예를 들어, 작성된 모든 문서를 `./docs` 디렉토리에 보관하고 그룹화된 섹션은 `./docs/ui-components` 및 `./docs/utilities` 와 같은 하위 디렉토리에 보관합니다. 이것은 우리에게 다음과 같은 조직을 제공합니다.

```
+-- ..
|-- (Jekyll files)
|
|-- docs
|   |-- ui-components
|   |   |-- index.md  (parent page)
|   |   |-- buttons.md
|   |   |-- code.md
|   |   |-- labels.md
|   |   |-- tables.md
|   |   +-- typography.md
|   |
|   |-- utilities
|   |   |-- index.md      (parent page)
|   |   |-- color.md
|   |   |-- layout.md
|   |   |-- responsive-modifiers.md
|   |   +-- typography.md
|   |
|   |-- (other md files, pages with no children)
|   +-- ..
|
|-- (Jekyll files)
+-- ..
```

부모 페이지 `YAML front matter parameter`에 다음을 추가한다 :
- `has_children: true` (부모 페이지임을 나타낸다)


#### Example
{: .no_toc }

```yaml
---
layout: default
title: UI Components
nav_order: 2
has_children: true
---

```

여기서는 `/docs/ui-components`에서 사용할 수 있는 `UI Components`의 랜딩 페이지를 설정하며, 이 페이지는 하위 항목이 있으며 기본 탐색에서 `두 번째`로 정렬됩니다.

---

## Child pages(자식 페이지)

자식 페이지에서는 YAML front matter의 `parent:` 매개변수를 `부모의 페이지 title`으로 설정하고 `nav_order` 를 설정하기만 하면 됩니다(이 숫자는 이제 섹션 내에서 범위가 지정됨).


#### Example
{: .no_toc }

```yaml
---
layout: default
title: Buttons
parent: UI Components
nav_order: 2
---

```

`Buttons page` 는 `UI Components` 의 자식으로 나타나며 `UI Components` 의 섹션에서 두 번째로 나타납니다.


### Ordering child pages(자식 페이지 순서 매기기)

옵션으로 `YAML front matter` 에 다음을 추가하여 자식 페이지의 기본 정렬 순서를 오름차순에서 내림차순으로 변경할 수 있습니다.
- `child_nav_order: desc`


#### Example
{: .no_toc }

```yaml
---
layout: default
title: Descending Child Pages
child_nav_order: desc
---
```

### Auto-generating Table of Contents(TOC 자동생성)

기본적으로 자식이 있는 모든 페이지는 부모 페이지의 콘텐츠 뒤에 자식 페이지를 나열하는 목차(`TOC`)를 자동으로 추가합니다. 이 자동 목차를 사용하지 않도록 설정하려면 `YAML front matter` 에서 `has_toc: false`를 설정합니다.


#### Example
{: .no_toc }

```yaml
---
layout: default
title: UI Components
nav_order: 2
has_children: true
has_toc: false
---

```

### Children with children(자식을 갖은 자식 페이지)

자식 페이지는 또한 자식(손자)를 가질 수 있다. 이는 자식 및 손자 페이지에서 유사한 패턴을 사용하여 수행됩니다.
1.	자식에 `has_children` 속성 추가
1.	손자에 `parent` 및 `grand_parent` 속성 추가

#### Example
{: .no_toc }

```yaml
---
layout: default
title: Buttons
parent: UI Components
nav_order: 2
has_children: true       
---

```

```yaml
---
layout: default
title: Buttons Child Page
parent: Buttons
grand_parent: UI Components  
nav_order: 1
---

```


이는 다음 탐색 구조를 만들 것이다 :

```
+-- ..
|
|-- UI Components
|   |-- ..
|   |
|   |-- Buttons
|   |   |-- Button Child Page
|   |
|   |-- ..
|
+-- ..
```

{: .note }
navigation structure는 3 levels로 제한됨: grandchild page는 child page를 가질 수 없다.

---


## Auxiliary Links(보조 링크)

사이트에 보조 링크를 추가하려면(모든 페이지의 오른쪽 상단에 있음) `_config.yml` 파일에 있는 `aux_links` 옵션에 추가합니다.


#### Example
{: .no_toc }

```yaml
# Aux links for the upper right navigation
aux_links:
  "Just the Docs on GitHub":
    - "//github.com/just-the-docs/just-the-docs"
```

---

## External Navigation Links( 외부 탐색 링크 )

탐색에 외부 링크를 추가하려면 사이트의 `_config.yml` 파일에 있는 `nav_external_links` 구성 옵션에 추가합니다.    
외부 링크는 일반 페이지에 대한 링크 뒤의 탐색에 나타나지만 컬렉션 앞에 나타납니다.


#### Example
{: .no_toc }

```yaml
# External navigation links
nav_external_links:
  - title: Just the Docs on GitHub
    url: https://github.com/just-the-docs/just-the-docs
    hide_icon: false # set to true to hide the external link icon - defaults to false
```


외부 링크는 내부 링크와 구별되는 아이콘으로 장식됩니다. `hide_icon: true` 를 설정하여 아이콘을 표시하지 않을 수 있습니다.

---

## In-page navigation with Table of Contents (목차를 사용한 페이지 내 탐색)

목차를 생성하려면 `Kramdown`의 {:toc} 메서드를 (마크다운 `<ol>`  바로 뒤에 있는 ) 사용할 수 있습니다. 이렇게 하면 `heading(제목)` 및 `heading level(제목 수준)`에 따라 페이지의 다양한 섹션에 대한 `anchor link(앵커 링크)`의 정렬된 `목록(TOC)`이 자동으로 생성됩니다. `heading`을 사용하고 `목차`에 표시하지 않으려는 경우가 있을 수 있으므로 특정 `heading`을 건너뛰려면 `{: .no_toc }` CSS class를 사용합니다.

#### Example
{: .no_toc }

```markdown
# Navigation Structure
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
```


이 예에서는 목차에서 heading 1 level(#)를 제외하고 목차 자체의 머리글(##)을 제외합니다. 순서가 지정되지 않은 목록을 가져오려면 `1. TOC`을 `- TOC`로 바꿉니다. 

### Collapsible Table of Contents(접을 수 있는 목차)
 
목차는 `<details>` `<summary>` 요소를 사용하여 접을 수 있습니다. 
open 속성(기본: 확장)과 `{: .text-delta }`로 스타일 지정은 선택 사항입니다.

```markdown
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>
```

{: .note }
{:toc}는 각 페이지에서 한 번만 사용할 수 있음.

