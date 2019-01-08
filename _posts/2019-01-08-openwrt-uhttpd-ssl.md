# ssl

OpenWRT uhttpd 에 SSL 적용 하기 위해서는  
cert1.pem 를 uhttpd.crt 로  
privkey1.pem 를 uhttpd.key 로  

```bash
openssl x509 -outform der -in cert1.pem -out uhttpd.crt
openssl rsa -outform der -in privkey1.pem -out uhttpd.key
```
