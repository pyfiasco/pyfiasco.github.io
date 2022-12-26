---
layout: default
title: Python
nav_order: 2
has_children: true
---

# Python

<h1>{{ "Hello World!" | downcase }}</h1>

<a href="http://localhost:4000/about.html" target="_blank" data-proofer-ignore>http://localhost:4000/about.html</a>


<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.url }} - {{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

{% for category in site.categories %}
  <h3>{{ category[0] }}</h3>
  <ul>
    {% for post in category[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}



<ul>
  {% highlight py linenos %}
  def foo
    puts 'foo'
  end
  {% endhighlight %}
</ul>




```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

New Label
{: .label .label-red }
```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

<div class="code-example" markdown="1">

[Link button](http://example.com/){: .btn }

</div>
```markdown
[Link button](http://example.com/){: .btn }

```


<font color='red-300'> 예쁜 파랑 </font>
<mark >예쁜 파랑 </mark>
