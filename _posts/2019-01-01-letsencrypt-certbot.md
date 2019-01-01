---
layout: post
title: Let's Encrypt with certbot and keytool
date:  2019-01-01 18:24:00 
categories: [SSL, certbot, DNS, spring boot]
---

# Let's Encrypt with certbot and keytool

Spring Boot 에 https 적용을 해보자 

certbot 인증방법
- standalone  
 임시 웹서버를 동작해서 인증  
 해당 서버에 웹서버 동작중일 경우 중지 해야 함
- webroot  
 웹서버 소스 폴더에 파일 생성 해서 인증 웹서버 중지 필요 없음
- manual  
 DNS 서버에 txt 정보를 입력 해서 인증 더큰 장점은 현재 운영중인 서버에 작업을 안해도됨  
 하지만 3개월 마다 1번씩 작업을 해야한다면?  
 내 최종 목적은 spring boot 에도 적용해야 하는됭 그럼?  

standalone, webroot 는 먼가 서버에 작업 한다는것이 좀 귀찮음  
지금은 manual dns 에 txt 값 2개만 등록 해주면 끝 이게 더 편해보임  

작업 순서
1. certbot 설치 
1. certbot --manaul 이용한 pem 생성
1. openssl 이용한 p12 생성
1. keytool 이용한 jks 생성
1. spring boot 에 적용


## 1. 작업

### 1.1 Certbot pem 파일 생성
```bash
root@linux:~$ sudo certbot certonly \
> --manual \
> --preferred-challenges=dns \
> --email user@gmail.com \
> --server https://acme-v02.api.letsencrypt.org/directory \
> --agree-tos \
> --debug \
> --no-bootstrap \
> -d domain.com \
> -d *.domain.com
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator manual, Installer None
Obtaining a new certificate
Performing the following challenges:
dns-01 challenge for domain.com
dns-01 challenge for domain.com

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
NOTE: The IP of this machine will be publicly logged as having requested this
certificate. If you're running certbot in manual mode on a machine that is not
your server, please ensure you're okay with that.

Are you OK with your IP being logged?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: y

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please deploy a DNS TXT record under the name
_acme-challenge.domain.com with the following value:

xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx1

Before continuing, verify the record is deployed.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Press Enter to Continue

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please deploy a DNS TXT record under the name
_acme-challenge.domain.com with the following value:

xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx2

Before continuing, verify the record is deployed.
(This must be set up in addition to the previous challenges; do not remove,
replace, or undo the previous challenge tasks yet. Note that you might be
asked to create multiple distinct TXT records with the same name. This is
permitted by DNS standards.)

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Press Enter to Continue
Waiting for verification...
Cleaning up challenges

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/zzizily.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/zzizily.com/privkey.pem
   Your cert will expire on 2019-04-01. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot
   again. To non-interactively renew *all* of your certificates, run
   "certbot renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le

root@linux:~$ cd /etc/letsencrypt
```

### 1.2 openssl, keytool(${JDK_HOME}/bin/keytool)

```bash
openssl pkcs12 -export -in cert.pem -inkey privkey.pem -out cert_and_key.p12 -name zzizily -CAfile chain.pem -caname zzizily
password 입력 
password 재입력


keytool -importkeystore -deststorepass ${PASSWORD} -destkeypass ${PASSWORD} -destkeystore letsencrypt.jks -srckeystore cert_and_key.p12 -srcstoretype PKCS12 -alias zzizily

keytool -importkeystore -destkeystore letsencrypt.jks -srckeystore letsencrypt.jks -deststoretype pkcs12
```

### 1.3 spring boot application.yml

jks 파일을 생성 했으면 spring boot 에 적용

```yml
server:
  ssl:
    key-store: classpath: letsencrypt.jks
    key-store-password: ${PASSWORD}
    key-password: ${PASSWORD}
```

![Spring Boot SSL 적용](https://user-images.githubusercontent.com/8334910/50573012-ec66c580-0e0e-11e9-83a7-609bbf39689d.png)


## 2. 작업중 문제점 발생

### 2.1 zsh
```zsh
root@linux:~$ sudo certbot certonly \
> --manual \
> --preferred-challenges=dns \
> --email user@gmail.com \
> --server https://acme-v02.api.letsencrypt.org/directory \
> --agree-tos \
> --debug \
> --no-bootstrap \
> -d domain.com \
> -d *.domain.com

zsh: no matches found: *.domain.com
```
zsh: no matches found: *.domain.com 진행 안됨

### 2.2 dns txt record 등록 

_acme-challenge 2개를 입력 해주어야함 google domain 에서는 + 아이콘이 있어서 복수 입력 가능  
dns 업체별로 방식이 다름 aws 에서는 복수 열로 입력이 가능 해서 뛰어쓰기로 구분

## 숙

3개월 마다 한번씩 자동화 하기?

## 참조
- [How to use Let's Encrypt DNS challenge validation?](https://serverfault.com/questions/750902/how-to-use-lets-encrypt-dns-challenge-validation)
- [Certbot으로 만든 인증서를 Spring Boot에서 사용하기](https://elfinlas.github.io/2018/03/19/spring-boot-tls-certbot)
