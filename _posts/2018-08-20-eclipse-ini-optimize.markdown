---
layout: post
title:  Eclipse ini 최적화 하기
date:   2018-08-20 23:54:00 +0900
categories: [Eclipse]
tags: [Eclipse, JVM]
---
# eclipse.ini

    -Xverify:none             #class 유효성 검사 생략
    -XX:+UseParallelGC        #GC 병렬 처리
    -XX:+AggressiveOpts       #컴파일러 소수점 기능 활성화 
    -XX:-UseConcMarkSweepGC   #GUI 응답을 빠르게 하기 openjdk 에서는 오류 발생 
    -XX:PermSize=512M         #
    -XX:MaxPermSize=51 2M      #
    -XX:NewSize=512M          #
    -XX:MaxNewSize=512M       #
    -Xms1024m                 #최소 Heap 메모리
    -Xmx1024m                 #최대 Heap 메모리

# JVM
* Permanent: JVM Class 와 Method 를 위한 공간
* New/Young: 새로 생성된 객체를 위한 공간
* Old: 만들어진지 오래된 객체들의 공간 (New 에서 옴)


# 참조
* [Eclipse 성능개선 최적화](https://www.slipp.net/wiki/pages/viewpage.action?pageId=5177633)
* [이클립스 속도 향상 (eclipse.ini 수정)](http://goddaehee.tistory.com/20)