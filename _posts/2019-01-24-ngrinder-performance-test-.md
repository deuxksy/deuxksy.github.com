---
layout: post
title: Web Site nGrinder Performance Test
date:  2019-01-24 11:44:00 
categories: [naver,nGrinder,Performance]
---
# 웹사이트 성능 테스트

웹사이트에 성능 테스트를 하기 좋은 방법은 멀까?  
간단하게 cli 에서 할수 있는 [loadtest](https://www.npmjs.com/package/loadtest), [artillery](https://www.npmjs.com/package/artillery) nodejs 기반으로 npm 으로 설치 가능 
좀더 고급 기능을 필요하다면 [jmeter](https://jmeter.apache.org/)  
하지만 나는 Web GUI 가능 하다면 최고지 라고 생각하다 알게된 [ngrinder](https://github.com/naver/ngrinder) 네이버 에서 별게 다 있구나  
war 파일로 제공을 하기 때문에 WAS 가 필요 쉬운

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


## 참고
[brownbears.tistory.com](https://brownbears.tistory.com/category/nGrinder)
