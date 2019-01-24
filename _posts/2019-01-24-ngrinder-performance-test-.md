---
layout: post
title: Web Site nGrinder Performance Test
date:  2019-01-24 11:44:00 
categories: [naver,nGrinder,Performance]
---
# 웹사이트 성능 테스트

웹사이트에 성능 테스트를 하기 좋은 방법은 멀까?  
간단하게 cli 에서 할수 있는 [loadtest](https://www.npmjs.com/package/loadtest), [artillery](https://www.npmjs.com/package/artillery) nodejs 기반 설치 및 기능 확장성이 좋음  
하지만 기능적인 측면 보다는 관리가 용이하고 Web GUI 우선이라서 알게된 [ngrinder](https://github.com/naver/ngrinder) 네이버~ 아! 좋다~

## 목차

1. 설치
2. 계정
3. 한글
4. 에이전트 설치 및 실행
5. 간단한 테스트
6. 

## 1. [설치](https://github.com/naver/ngrinder/wiki/Installation-Guide)
WAS/webapps/ngrinder.war 설치  
localhost:8080/ngrinder 접속 기본 계정 및 비밀번호 admin/admin  
![01](https://user-images.githubusercontent.com/8334910/51687151-4d13a780-2035-11e9-8762-b46218747399.png)
[ngrinder architechture](https://github.com/naver/ngrinder/wiki/Architecture)


## 참고
- [ngrinder brownbears.tistory.com](https://brownbears.tistory.com/category/nGrinder)
- [artillery 이용한 스트레스 테스트](https://blog.outsider.ne.kr/1238)
