---
layout: post
title:  Installing on tomcat with gerrit.war
date:   2018-12-10 18:02:00
categories: [gerrit, code review, install]
---
# Tomcat 을 이용해서 Gerrit 설치 하기

[Gerrit](https://www.gerritcodereview.com/) 두가지 방법으로 설치가 가능

- war 를 tomcat 에 넣기
- java -jar gerrit.war init -d /path/to/your/gerrit_application_directory

별도의 설치 과정을 거치지 않고 ${Tomcat}/webapps 폴더에 넣어서 설치 하고 싶음 war 파일로 배포하자나  
[설치 가이드](https://gerrit-documentation.storage.googleapis.com/Documentation/2.16.1/install-j2ee.html) 있지만 친절 하지가 않음 특히 ***gerrit-2.16, gerrit-2.15 버전은 버그가 있어서 설치가 안됨***  
gerrit-2.14.17 설치가 가능함 이하 버전은 확인 안함

- gerrit-2.16 오류 발생 class not loader ...  
- gerrit-2.15 오류 발생 No implementation for com.google.gerrit.audit.AuditService was bound ...  

## 1 설치

### 1.1. DB 설정

${tomcat}/conf/context.xml

```xml
<Resource
  name="jdbc/ReviewDb"
  type="javax.sql.DataSource"
  username="${user.id}"
  password="${user.password}"
  driverClassName="org.mariadb.jdbc.Driver"
  url="jdbc:mariadb://${host}:${port}/${db}?autoReconnect=true"
/>
```

### 1.2. DB 생성

[설치 가이드](https://gerrit-documentation.storage.googleapis.com/Documentation/2.16.1/install-j2ee.html) 를 보면 [site initialization](https://gerrit-documentation.storage.googleapis.com/Documentation/2.16.1/install.html#init) 진행 해야 한다고 나옴 왜 해야 하지 하기 싫어 Tomcat 으로 하는되  
진행 하니 [site initialization](https://gerrit-documentation.storage.googleapis.com/Documentation/2.16.1/install.html#init) 과정을 거치면 Table Data 생성 작업이 진행됨

### 1.3. gerrit.war tomcat/webapps 폴더에 복사

gerrit.war 파일을 tomcat/webapps 넣어 주면 끝