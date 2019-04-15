---
layout: post
title: Java 8 functional interface
date:  2019-04-15 23:29:00 
categories: [micro-service, develop, java, spring-cloud, netflix]
---
# Developing a micro-service in a local environment
micro-service 를 local 환경에서 개발하기 하기 위해서는 기존 monolithic 과는 많이 다르다.  
**운영 환경 와 동일한 환경으로 개발을 하기 위해서는 어떻게 해야 할까?**

Spring Cloud, Netflix OSS 를 활용 한다면 4개의 어플리케이션이 필수 요소 이다.
- Discovery (Eureka)
- API Gateway (Spring Cloud Gateway)  
- API (api-skeleton)
- Client (client-skeleton)

Client 만 개발시에는 API 가 필요 하지 않기 때문에 dev 환경에 API 가 동작 한다는 전제를 한다.  
환경은 2 가지만 생각을 해보자
- local
- dev

현재 4 가지 상황이 있고 더 추가 될수 있다.

## 목차
- Client (홈페이지)
- API (기능)
- API & API
- Client & API

## Clinet (홈페이지)
Client 만 개발 한다.  
dev 환경의 API Gateway 통해서 가지고 오면 된다.  
**독립**적으로 개발이 가능 하다.  
Client 모듈만 필요

## API (기능)
API 만 개발 한다.  
API 에는 개발을 위한 소스가 있다. 
**독립**적으로 개발이 가능 하다.
API 모듈만 필요

## API & API
API A 와 API B 를 같이 개발 한다.  
A 와 B 는 서로 간에 Discovery 가 필요하기 때문에 Eureka 사용이 필요하다.  
API A, API B, Eureka 3가지 모듈 필요

## Client & API
Client 와 API 둘다 개발 한다.  
외부에 있는 Client 가 내부에 있는 API 통하기 이해서는 Gateway 가 필요하다.
Client, API, Gateway 3가지 모듈 필요
