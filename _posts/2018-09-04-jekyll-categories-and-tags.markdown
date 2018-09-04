---
layout: post
title: Github Page 로 Jekyll 을 Categories 와 Tags 설정하기
date: 2018-09-04 23:51:00
categories: [jekyll]
---
/categories.md 생성

```
---
layout: page
title: Categories
permalink: /categoreis/
---

{% for category in site.categories %}
    <div class="archive-group">
      {% capture category_name %}{{ category | first }}{% endcapture %}
      <h3 class="category-head">{{ category_name }}</h3>
      {% for post in site.categories[category_name] %}
      <article class="archive-item">
        <h4><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a></h4>
      </article>
      {% endfor %}
    </div>
{% endfor %}
```

## 참조
* [3 Simple Steps To Setup Jekyll Categories And Tags](https://blog.webjeda.com/jekyll-categories/)`