# OpenSSL
- SSL(Secure Socket Layer)
- www 브라우저와 web 서버 간에 데이터를 안전하게 주고 받기 위한 업계 표준 프로토콜
- HTTPS를 위해서 인증서 발급을 위해 openssl 사용
- 무료라 그런지 조금의 보안이슈가..

## Generating the Private Key
```bash
$ openssl genrsa -out private.key 1024
```

## Generating the Public Key
```bash
$ openssl rsa -in private.key -out public.pem -pubout -outform PEM
```
