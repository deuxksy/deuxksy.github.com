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
1. certbot 인증서 생성
1. openssl 이용한 p12 생성, keytool 이용한 jks 생성
1. spring boot 에 적용
1. 작업중 문제점

## 1. certbot 설치

```bash
# yum install certbot
Loaded plugins: fastestmirror, priorities
Loading mirror speeds from cached hostfile
 * base: mirror.navercorp.com
 * epel: ftp.riken.jp
 * extras: mirror.navercorp.com
 * remi-safe: ftp.riken.jp
 * rpmforge: ftp.neowiz.com
 * updates: mirror.navercorp.com
 * webtatic: us-east.repo.webtatic.com

... 중략 ...

Installed:
  certbot.noarch 0:0.29.1-1.el7

Dependency Installed:
  audit-libs-python.x86_64 0:2.8.4-4.el7         checkpolicy.x86_64 0:2.5-8.el7                  libcgroup.x86_64 0:0.41-20.el7               libsemanage-python.x86_64 0:2.5-14.el7        policycoreutils-python.x86_64 0:2.5-29.el7
  pyOpenSSL.x86_64 0:0.13.1-4.el7                python-IPy.noarch 0:0.75-6.el7                  python-cffi.x86_64 0:1.6.0-5.el7             python-enum34.noarch 0:1.0.4-1.el7            python-idna.noarch 0:2.4-1.el7
  python-ndg_httpsclient.noarch 0:0.3.2-1.el7    python-ply.noarch 0:3.4-11.el7                  python-pycparser.noarch 0:2.14-1.el7         python-requests.noarch 0:2.6.0-1.el7_1        python-requests-toolbelt.noarch 0:0.8.0-1.el7
  python-six.noarch 0:1.9.0-2.el7                python-zope-component.noarch 1:4.1.0-3.el7      python-zope-event.noarch 0:4.0.3-2.el7       python-zope-interface.x86_64 0:4.0.5-4.el7    python2-acme.noarch 0:0.29.1-1.el7
  python2-certbot.noarch 0:0.29.1-1.el7          python2-configargparse.noarch 0:0.11.0-1.el7    python2-cryptography.x86_64 0:1.7.2-2.el7    python2-future.noarch 0:0.16.0-6.el7          python2-josepy.noarch 0:1.1.0-1.el7
  python2-mock.noarch 0:1.0.1-9.el7              python2-parsedatetime.noarch 0:2.4-5.el7        python2-pyasn1.noarch 0:0.1.9-7.el7          python2-pyrfc3339.noarch 0:1.0-2.el7          python2-requests.noarch 0:2.6.0-0.el7
  python2-six.noarch 0:1.9.0-0.el7               pytz.noarch 0:2016.10-2.el7                     setools-libs.x86_64 0:3.3.8-4.el7

Failed:
  python-urllib3.noarch 0:1.10.2-5.el7

[root@devops-service-pig ~]# certbot certonly \
> --manual \
> --preferred-challenges=dns \
> --email user@gmail.com \
> --server https://acme-v02.api.letsencrypt.org/directory \
> --agree-tos \
> --debug \
> --no-bootstrap \
> -d tricycle.co.kr \
> -d *.tricycle.co.kr
Traceback (most recent call last):
  File "/bin/certbot", line 9, in <module>
    load_entry_point('certbot==0.29.1', 'console_scripts', 'certbot')()
  File "/usr/lib/python2.7/site-packages/pkg_resources/__init__.py", line 487, in load_entry_point
    return get_distribution(dist).load_entry_point(group, name)
  File "/usr/lib/python2.7/site-packages/pkg_resources/__init__.py", line 2728, in load_entry_point
    return ep.load()
  File "/usr/lib/python2.7/site-packages/pkg_resources/__init__.py", line 2346, in load
    return self.resolve()
  File "/usr/lib/python2.7/site-packages/pkg_resources/__init__.py", line 2352, in resolve
    module = __import__(self.module_name, fromlist=['__name__'], level=0)
  File "/usr/lib/python2.7/site-packages/certbot/main.py", line 20, in <module>
    from certbot import account
  File "/usr/lib/python2.7/site-packages/certbot/account.py", line 18, in <module>
    from acme import messages
  File "/usr/lib/python2.7/site-packages/acme/messages.py", line 8, in <module>
    from acme import challenges
  File "/usr/lib/python2.7/site-packages/acme/challenges.py", line 12, in <module>
    import requests
  File "/usr/lib/python2.7/site-packages/requests/__init__.py", line 58, in <module>
    from . import utils
  File "/usr/lib/python2.7/site-packages/requests/utils.py", line 32, in <module>
    from .exceptions import InvalidURL
  File "/usr/lib/python2.7/site-packages/requests/exceptions.py", line 10, in <module>
    from .packages.urllib3.exceptions import HTTPError as BaseHTTPError
  File "/usr/lib/python2.7/site-packages/requests/packages/__init__.py", line 95, in load_module
    raise ImportError("No module named '%s'" % (name,))
ImportError: No module named 'requests.packages.urllib3'
```

가끔 python-urllib3.noarch 0:1.10.2-5.el7 설치가 실패 하는 경우 certbot 동작이 안됨  
기존 설치된 라이브러스 삭제 후 재설치  

```bash
pip uninstall requests urllib3
yum remove python-urllib3 python-requests
yum install python-urllib3 python-requests certbot
```

## 2. Certbot 인증서 생성
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

- privkey.pem: 개인키
- cert.pem: example.com 도메인 인증서
- chain.pem: CA(The Let’s Encrypt) 기관 체인 인증서
- fullchain.pem(cert.pem + chain.pem): 도메인의 인증서와 CA 기관 인증서

## 3. openssl, keytool(${JDK_HOME}/bin/keytool)

```bash
openssl pkcs12 -export -in cert.pem -inkey privkey.pem -out cert_and_key.p12 -name zzizily -CAfile chain.pem -caname zzizily
password 입력 
password 재입력


keytool -importkeystore -deststorepass ${PASSWORD} -destkeypass ${PASSWORD} -destkeystore letsencrypt.jks -srckeystore cert_and_key.p12 -srcstoretype PKCS12 -alias zzizily

keytool -importkeystore -destkeystore letsencrypt.jks -srckeystore letsencrypt.jks -deststoretype pkcs12
```

## 4. spring boot application.yml

jks 파일을 생성 했으면 spring boot 에 적용

```yml
server:
  ssl:
    key-store: classpath: letsencrypt.jks
    key-store-password: ${KEY-STORE-PASSWORD}
    key-password: ${KEY-PASSWORD}
```

![Spring Boot SSL 적용](https://user-images.githubusercontent.com/8334910/50573012-ec66c580-0e0e-11e9-83a7-609bbf39689d.png)


## 5. 작업중 문제점

### 5.1 zsh
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

### 5.2 dns txt record 등록 

_acme-challenge 2개를 입력 해주어야함 google domain 에서는 + 아이콘이 있어서 복수 입력 가능  
dns 업체별로 방식이 다름 aws 에서는 복수 열로 입력이 가능 해서 뛰어쓰기로 구분

## 숙제

3개월 마다 한번씩 자동화 하기?

## 참조
- [How to use Let's Encrypt DNS challenge validation?](https://serverfault.com/questions/750902/how-to-use-lets-encrypt-dns-challenge-validation)
- [Certbot으로 만든 인증서를 Spring Boot에서 사용하기](https://elfinlas.github.io/2018/03/19/spring-boot-tls-certbot)
