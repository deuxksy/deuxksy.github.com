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
 웹서버 미사용 상태에서 임시 웹서버를 동작해서 인증
- webroot
 웹서버 소스 폴더에 파일생성 해서 인증
- manual
 수동으로 이것저것 해서 인증

standalone, webroot 는 먼가 서버에 작업 한다는것이 좀 귀찮음
manual dns 에 txt 값 2개만 등록해주면됨 이게더 편하겠네

'''bash
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

root@linux:~$ cd /etc/letsencrypt/
'''



덧. zsh 에서 *.domain.com 하니깐 zsh: no matches found: *.domain.com 경고 창이 뜨면서 진행 안됨  
덧덧. dns 서버에 _acme-challenge 등록시 2개 이상 입력 해주어야함 google domain 에서는 + 아이콘이 있어서 복수 
