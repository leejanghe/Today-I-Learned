# 세션 스프린트

---

# 기본설정

## 1. 환경변수 설정

기본 설정은 세션스프린트에 나와있기 때문에 생략!

<br />

# Server

## 1. https 인증서 가져오기

```
$ mkcert -key-file key.pem -cert-file cert.pem localhost 127.0.0.1 ::1
```

위와 같이 사설 인증서를 발급하면 개인키 공개키 파일이 생성됩니다.

<br />