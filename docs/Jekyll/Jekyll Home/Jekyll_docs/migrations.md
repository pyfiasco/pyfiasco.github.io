---
layout: default
title: migration
parent: Jekyll_docs
grand_parent: Jekyll Home
---

# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

<!--
If you’re switching to Jekyll from another blogging system, Jekyll’s importers
can help you with the move. To learn more about importing your site to Jekyll,
visit our [`jekyll-import` docs site](https://import.jekyllrb.com/docs/home/).
-->
만약 다른 블로그 시스템으로부터 Jekyll 로 전환하려고 한다면, Jekyll 의 임포트
기능을 유용하게 사용할 수 있습니다. 자신의 사이트를 Jekyll 로 가져오는 방법을
알아보려면, [`jekyll-import` 문서 사이트](https://import.jekyllrb.com/docs/home/)를 방문해보세요.

## Getting started
If you’re switching to Jekyll from another blogging system, Jekyll’s importers can help you with the move. Most methods listed on this page require read access to the database from your old system to generate posts for Jekyll. Each method generates .markdown posts in the _posts directory based on the entries in the foreign system.

Other Systems
If you have a system for which there is currently no migrator, consider writing one and sending us [a pull request](https://github.com/jekyll/jekyll-import).


## Installation
Because the importers have many of their own dependencies, they are made available via a separate gem called [jekyll-import](https://github.com/jekyll/jekyll-import). To use them, all you need to do is install the gem, and they will become available as part of Jekyll’s standard command line interface.

```
$ gem install jekyll-import
```

{: .warning}
> Jekyll-import requires you to manually install some dependencies.
Most importers require one or more dependencies. In order to keep `jekyll-import`'s footprint small, we don't bundle the gem with every plausible dependency. Instead, you will see a nice error message describing any missing dependency and how to install it. If you're especially savvy, take a look at the `require_deps` method in your chosen importer to install all of the deps in one go.

## Usage
You should now be all set to run the importers with the following incantation:

```
$ ruby -r rubygems -e 'require "jekyll-import";
    JekyllImport::Importers::MyImporter.run({
      # options for this importer
    })'
```

Where `MyImporter` is the name of the specific importer.

{: .note}
> Always double-check migrated content
Importers may not distinguish between published or private posts, so you should always check that the content Jekyll generates for you appears as you intended.


## Behance   

{: .note}
> Additional Dependencies
This importer requires the following additional libraries.
 - [behance](https://rubygems.org/gems/behance)
 - [safe_yaml](https://rubygems.org/gems/safe_yaml)
You may install the needed gems individually by running gem install GEM_NAME or install all of them with a single invocation:gem install behance safe_yaml

### Invocation   

Sample snippet to invoke the importer:

```
jekyll import behance --user NAME --api_token TOKEN
```

<div class="mobile-side-scroller">
<table>
  <thead>
    <tr>
      <th>OPTION</th>
      <th class="filter">DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
      <tr>
        <td>
          <code>--user NAME</code>
        </td>
        <td>
          The username of the account
        </td>
      </tr>
      <tr>
        <td>
          <code>--api_token TOKEN</code>	
        </td>
        <td>
          The API access token for the account
        </td>
      </tr>
  </tbody>
</table>
</div>

\* Highlighted row(s) in table above indicate required options.

[View Source →](https://github.com/jekyll/jekyll-import/blob/v0.14.0/lib/jekyll-import/importers/behance.rb)



## [others](https://import.jekyllrb.com/docs/blogger/)




