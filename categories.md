---
layout: page
title: Categories
permalink: /categoreis/
---
{% for post in site.categories[page.category] %}
    <a href="{{ post.url | absolute_url }}">
      {{ post.title }}
    </a>
{% endfor %}