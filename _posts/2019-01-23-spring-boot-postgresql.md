---
layout: post
title: Spring Boot PostgreSQL SQLFeatureNotSupportedException
date:  2019-01-23 09:35:00 
categories: [spring boot,postgresql]
---

# Spring Boot PostgreSQL SQLFeatureNotSupportedException

## 원인

JPA(Hibernate) 가 PostgreSQL CLOB 기능을 확인 하지만 실제 기능 제공 안하면서 발생함

- [Spring Boot issues 12007](https://vkuzel.com/spring-boot-jpa-hibernate-atomikos-postgresql-exception)
- [HHH-12368](https://hibernate.atlassian.net/browse/HHH-12368)

## 해결방법

### 1. logging.level 변경

```yml
logging:
  level:
    org.hibernate.engine.jdbc.env.internal.LobCreatorBuilderImpl: ERROR
```

### 2. jpa 설정

```yml
spring:
  jpa:
    properties:
      hibernate:
        jdbc:
          lob:
            non_contextual_creation: true
```

### 3. 기능감지 비활성화후 수동 설정

```yml
spring:
  jpa:
    properties:
      hibernate:
        temp:
          use_jdbc_metadata_defaults: false
    database-platform: org.hibernate.dialect.PostgreSQL9Dialect
```
