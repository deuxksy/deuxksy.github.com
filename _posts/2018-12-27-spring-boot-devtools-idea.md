---
layout: post
title: Spring Boot DevTools IDEA 설정
date:   2018-12-27 16:25:00
categories: [IDEA, Spring Boot]
---

# Spring Boot DevTools IDEA 설정

Spring Boot DevTools 사용하면 resources 나 class 변경시 자동으로 반영이 된다.  
Eclipse 에서는 별다른 설정없이 가능 하지만 IDEA 에서는 추가 설정이 필요하다.  

IDEA Ultimate 사용시에는 Run/Debug Configurations 에서 기능을 지원 편하게 사용할수 있지만  
IDEA Community 에서는 별도의 설정이 필요함  

## 1. [Chrome LiveReload 설치](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei)  

필수 사항은 아니지만 LiveReload 기능을 사용 하고 싶으면 설치 하고 활성화가 필요함

## 2. ctrl+alt+s > Build, Execution. Deployment > Compiler 

- [x] Build project automatically

![IDEA Compiler](https://user-images.githubusercontent.com/8334910/53310652-15787380-38f1-11e9-9501-20314afcca6b.png)

## 3. ctrl+shift+a > registry... 

- [x] compiler.automake.allow.when.app.runing
- [x] ide.windowSystem.autoShowProcessPopup
![IDEA Setting](https://user-images.githubusercontent.com/8334910/53310650-15787380-38f1-11e9-878b-625f7f92ee76.png)

## 4. application.yml

devtools.restart.enabled, devtools.livereload.enabled 두값 모두 true 기본값 그래도 미심적으니깐 설정
```yml
spring:
  devtools:
    restart:
      enabled: true
    livereload:
      enabled: true
```
