---
layout: post
title: Spring Boot HikariCP DataSource 등록 
date: 2018-09-06 18:00:00
categories: [Spring, Boot, DataSource, HikariCP]
---
기본적으로 Connection Pool Name 은 각각 어플 마다 다른 이름을 주어야함<br>
그 와는 별게로 1개의 Tomcat 에 2개 이상의 Context 를 사용시 HikariCP 로 DataSource 등록 이 실패함??<br>

## 원인
spring.jmx.default-domain 가 기본적으로 사용 그리고 별도의 값을 주지 않으면 동일한 이름 으로 사용이 안됨


## 해결
jmx 를 사용하지 않거나 default-domain 를 각 어플 마다 다른 값으로 설정 해야함

    spring:
        jmx:
            default-domain: ${UNIQUE}

## 참조
* https://stackoverflow.com/questions/27440985/unable-to-register-mbean-hikaridatasource-hikaripool-0-with-key-datasource
