---
layout: post
title: Maven Plugin Task List Check
date:  2019-01-31 09:24:00 
categories: [Maven, Plugin]
---
# Maven Plugin Task List Check

Maven 의 사용 중인 Plugin 들에 대한 Task (Goal) 확인 하기

```text
mvn help:describe -Dplugin=org.apache.maven.plugins:maven-war-plugin -Ddetail=true
```


## 참고
- [Configuring Describe Goal](https://maven.apache.org/plugins-archives/maven-help-plugin-LATEST/examples/describe-configuration.html)
- [Why are my contributions not showing up on my profile?](https://www.baeldung.com/maven-goals-phases)
