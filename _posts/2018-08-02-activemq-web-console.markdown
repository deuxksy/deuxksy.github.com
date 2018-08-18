---
layout: post
title:  ActiveMQ Web Console ID/PW 변경
date:   2018-08-02 22:38:39 +0900
categories: activemq
---
ActiveMQ Web Console ID/PW 변경
===
Active (5.14.5) 사용시 관리자 Web Console 이 있어서 Queue 와 Topic 모니터링이 용이 하다 <br/>
기본 ID/PW 는 admin / admin 이고 운영을 위해서는 변경이 필요<br/>

    %ACTIVEMQ_HOME%\conf\jetty-realm.properties
    #username: password, rolename
    admin: admin, admin
    user: user, user