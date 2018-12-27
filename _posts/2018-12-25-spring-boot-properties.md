---
layout: post
title:  Spring Boot Properties
date:   2018-12-25 08:30:00
categories: [spring,boot,properties]
---
# Spring Boot Properties

Spring Boot 의 모든 설정값 이라고 할수 있는 application.yml

## 위치 우선순위

1. --spring.config.location=${path}/application.yml
1. 실행 폴더 config/application.yml
1. 실행 폴더 application.yml
1. module.jar/config/application.yml
1. module.jar/application.yml


## 속성값 우선순위

1. java -jar module.jar --key=value
1. java -Dkey=value -jar module.jar
1. %key% or ${key}

### 참조

[DevKuma-프로퍼티 파일(properties)](http://www.devkuma.com/books/pages/501)
[DevKuma-속성파일 이외의 설정값 전달](http://www.devkuma.com/books/pages/504)
