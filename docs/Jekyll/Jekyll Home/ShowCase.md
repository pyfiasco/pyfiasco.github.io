---
layout: default
title: ShowCase
parent: Jekyll Home
grand_parent: Jekyll
---


<ul>
    {% for s in site.data.showcase %}
        <a href="{{ s.link }}">{{ s.name }}</a><br>
    {% endfor %}  
</ul>
