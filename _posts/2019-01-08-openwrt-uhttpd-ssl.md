---
layout: post
title: OpenWRT uHTTPd SSL 적용
date: 2019-01-08 23:51:00
categories: [OpenWRT,SSL,uHTTPd]
---

# OpenWRT uHTTPd SSL 적용

OpenWRT uhttpd 에 SSL 적용 하기 위해서는  
cert1.pem 를 uhttpd.crt 로  
privkey1.pem 를 uhttpd.key 로  

```bash
openssl x509 -outform der -in cert1.pem -out uhttpd.crt
openssl rsa -outform der -in privkey1.pem -out uhttpd.key
```

## 참조
[Convert .pem to .crt and .key](https://stackoverflow.com/questions/13732826/convert-pem-to-crt-and-key)
[How to convert .pem into .key?](https://stackoverflow.com/questions/19979171/how-to-convert-pem-into-key)
