---
layout: post
title:  ActiveMQ Account 으로 연결 하기
date:   2018-08-02 22:38:39 +0900
categories: activemq spring-boot
---
ActiveMQ Account 으로 연결 하기
===
# 1. ActiveMQ activemq-security.xml
ActiveMQ 는 기본 설정으로 Anonymous 로 연결이 가능 하다.<br/>
실제 서비스시에는 Anonymous 차단 하고 Queue 또는 Topic 에 Account 에 따른 정책이 필요함<br/>

Simple Authentication Plugin 이름으로 기능을 지원 예제 파일<br/>
${ACTIVEMQ_HOME}/example/conf/activemq-security.xml<br/>

    ${ACTIVEMQ_HOME}/conf/activemq.xml
    <plugins>
    <simpleAuthenticationPlugin>
    <users>
    <authenticationUser username=”${activemq.username}” password=”${activemq.password}” groups=”admins”/>
    </users>
    </simpleAuthenticationPlugin>
    <authorizationPlugin>
    <map>
    <authorizationMap>
    <authorizationEntries>
    <authorizationEntry queue=”>” read=”admins” write=”admins” admin=”admins” />
    <authorizationEntry topic=”>” read=”admins” write=”admins” admin=”admins” />
    </authorizationEntries>
    </authorizationMap>
    </map>
    </authorizationPlugin>
    </plugins>

# 2. Java (Spring Boot 1.5.x) 설정 추가
    ${SPRING_APPLICATION_YML}
    spring:
    activemq:
    broker-url: tcp://remotehost:61616
    user: bigmama
    password: qwe123

# 3. jasypt 지원 으로 암호화 가능
    ${ACTIVEMQ_HOME}/conf/credentials-enc.properties