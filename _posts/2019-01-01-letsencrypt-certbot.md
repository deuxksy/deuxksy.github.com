---
layout: post
title: Let's Encrypt with certbot
date:  2019-01-01 18:24:00 
categories: [SSL, certbot, DNS]
---

# Let's Encrypt with certbot

https 적용을 해보자

certbot 는 3가지 방법을 지원한다
- standalone  
 임시 웹서버를 동작해서 인증 인증서버에 웹서버 동작중일경우 중지해야함
- webroot  
 웹서버 소스 폴더에 파일생성 해서 인증
- manual  
 수동으로 이것저것 해서 인증 DNS 에 txt 정보만 입력 해서 사용 가능

standalone, webroot 는 먼가 서버에 작업 한다는것이 좀 귀찮음
manual dns 에 txt 값 2개만 등록해주면됨 이게더 편하겠네

## 1. 작업

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
openssl pkcs12 -export -in cert.pem -inkey privkey.pem -out cert_and_key.p12 -name zzizily -CAfile chain.pem -caname zzizily

keytool -importkeystore -deststorepass qwe123 -destkeypass qwe123 -destkeystore letsencrypt.jks -srckeystore cert_and_key.p12 -srcstoretype PKCS12 -alias zzizily

keytool -importkeystore -destkeystore letsencrypt.jks -srckeystore letsencrypt.jks -deststoretype pkcs12

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

## 참조
[How to use Let's Encrypt DNS challenge validation?](https://serverfault.com/questions/750902/how-to-use-lets-encrypt-dns-challenge-validation)
