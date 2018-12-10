---
layout: post
title:  Headless Browsers
date:   2018-12-10 18:02:00
categories: [Web Browser, Web Crawler]
---
# Headless Browsers

웹 페이지 크롤링 할때 라이브러리 선택

- 난 Java 로 해야 하고 가볍게 가고 싶어 무거운거 싫어
- 크롤링 하는 데이터가 HTML DOM 이라면 [Jsoup](https://jsoup.org/) 와 [Jaunt](https://jaunt-api.com/download.htm) 이거 상용이네 ㅡㅡ;;
- CSS Selector 기능이 있는 Jsoup 결정 할려다가 JavaScript 를 지원 해야 하는되
- 그렇다고 Selenium 으로 가자니 무겁고 그래서 결론은 [HtmlUnit](http://htmlunit.sourceforge.net/) CSS Selector는 물론 Xpath 도 지원

## 참조

[Headless Browsers](http://www.asad.pw/HeadlessBrowsers) or [GitHub](https://github.com/dhamaniasad/HeadlessBrowsers)