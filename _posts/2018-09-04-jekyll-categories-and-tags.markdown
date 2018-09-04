---
layout: post
title: Github Page 로 Jekyll 을 Categories 와 Tags 설정하기
date: 2018-09-04 23:51:00
categories: [jekyll]
---
/categories.md 생성

    ---
    layout: page
    title: Categories
    permalink: /categoreis/
    ---

&lbrace;&percnt; for category in site.categories &percnt;&rbrace;
    &lt;div class=&quot;archive-group&quot;&gt;
      &lbrace;&percnt; capture category_name &percnt;&rbrace;&lbrace;&lbrace; category | first &rbrace;&rbrace;&lbrace;&percnt; endcapture &percnt;&rbrace;
      &lt;h3 class=&quot;category-head&quot;&gt;&lbrace;&lbrace; category_name &rbrace;&rbrace;&lt;/h3&gt;
      &lbrace;&percnt; for post in site.categories[category_name] &percnt;&rbrace;
      &lt;article class=&quot;archive-item&quot;&gt;
        &lt;h4&gt;&lt;a href=&quot;&lbrace;&lbrace; site.baseurl &rbrace;&rbrace;&lbrace;&lbrace; post.url &rbrace;&rbrace;&quot;&gt;&lbrace;&lbrace;post.title&rbrace;&rbrace;&lt;/a&gt;&lt;/h4&gt;
      &lt;/article&gt;
      &lbrace;&percnt; endfor &percnt;&rbrace;
    &lt;/div&gt;
&lbrace;&percnt; endfor &percnt;&rbrace;


## 참조
* [3 Simple Steps To Setup Jekyll Categories And Tags](https://blog.webjeda.com/jekyll-categories/)