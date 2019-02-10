---
layout: post
title: download-all-images-of-a-website-using-wget
date:  2019-02-10 18:29:00 
categories: [java, 8, functional, interface]
---
# Download all images of a website using wget

특정 웹사이트의 모든 이미지를 다운로드 받기  

## 1. 목차

1. 방법
   1. chrome Image Downloader
   2. flashget
   3. httrack
   4. wget or curl
2. 참조

## 2. 방법

### 2.1. [Image Downloader](https://chrome.google.com/webstore/detail/image-downloader/cnpniohnfphhjihaiiggeabnkjhpaldj)

제일 만만한 방법이지만 웹페이지만 가능 해서 포기

### 2.2. [flashget](http://www.flashget.com/index_en.html)

어플을 설치해야 해서 포기

### 2.3. [httrack](https://www.httrack.com/)

어플 설치및 웹사이트 가 아닌 이미지만 받는게 목적이라서 포기

### 2.4. wget or curl

이게 될까 하고 잠깐 검색 하고 테스트 해바는됭 된다  
아 역시 대단하 1줄만 모든 이미지 다운 받기 성공

```bash
wget -nd -r -P /save/location -A jpeg,jpg,bmp,gif,png http://www.imge.com
```

[explainshell.com](https://explainshell.com/explain?cmd=wget+-nd+-r+-P+%2Fsave%2Flocation+-A+jpeg%2Cjpg%2Cbmp%2Cgif%2Cpng+http%3A%2F%2Fandar.co.kr)

## 3. 참조

[How do I use Wget to download all images into a single folder, from a URL?](https://explainshell.com/explain?cmd=wget+-nd+-r+-P+%2Fsave%2Flocation+-A+jpeg%2Cjpg%2Cbmp%2Cgif%2Cpng+http%3A%2F%2Fandar.co.kr)
[wget-image-scraper](https://github.com/eduardschaeli/wget-image-scraper)