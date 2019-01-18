---
layout: post
title: 403 Access Denied on Tomcat 8 Manager App without prompting for user/password
date:  2019-01-18 12:10:00 
categories: [Tomcat,Mananger]
---

# Tomcat Manager 접근 허용 

Tomcat Mananger 를 이용해서 webapp 관리를 해야함 그런데 403 이똭!!  
$CATALINA_HOME/webapps/manager/META-INF/context.xml 파일의 원격 적근 제한을 주석 처리  
누구나 들어 올수 있도록 설정  

```xml
<Context antiResourceLocking="false" privileged="true" >
<!--
<Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
-->
</Context>
```

## 참조
[403 Access Denied on Tomcat 8 Manager App without prompting for user/password](https://stackoverflow.com/questions/38551166/403-access-denied-on-tomcat-8-manager-app-without-prompting-for-user-password)
[Configuring Manager Application Access](http://tomcat.apache.org/tomcat-9.0-doc/manager-howto.html#Configuring_Manager_Application_Access)
