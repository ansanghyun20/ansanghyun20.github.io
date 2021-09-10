---
layout: post
title: Nginx 시행착오 정리
subtitle: Nginx 시행착오
categories: JavaScript
tags: [Web]
---

### Nginx?

Nginx는 웹서버, 프록시 기능을 가진 소프트웨어이다.

Nginx는 경량의 목표를 가졌고 `비동기` 이벤트 구조라고 한다.

1. Apache는 프로세스 스레드 기반이라서 사용자가 많아지면 느려지는 문제가 생긴다.
2. NginX 같은 경우에는 Event-Driven 구조를 가져 Apache 보다 많은 연결에 효과적이며 작은 쓰레드로 클라이언트 처리가 가능하다.


### 어떤 시행착오?

(flask)AI 서버를 사용해서 Client의 주기적인 요청에 응답해야하는 경우가 있었다.

http통신에 문제는 크게 없는 것으로 생각하였지만 https 통신에서 문제가 컸다.

1. http <-> https 통신은 안된다.
2. OpenSSL 인증서는 간혹 문제가 있어 환경에따라서 작동하지 않는다.
3. 2번 문항 또는 flask에 바로 ssl을 적용해서 문제가 생긴다.

### 어떻게 해결?

해결하는 방법은 프로젝트 진행하는 멘토님 께서 알려주셨다.

1. 80 포트와 443 포트를 사용한다.
2. 도메인을 산다. (Godaddy에서 구매하였다.)
3. https://sg.godaddy.com/offers/godaddy?isc=gofkkr12&countryview=1&currencyType=krw&gclsrc=aw.ds&gclid=Cj0KCQjw4eaJBhDMARIsANhrQAA2AH5QRov9MPtVbxV6Hhe7SBgZVz589u5jMtbkjkqJoWzyUhF3ELAaAhicEALw_wcB
4. 주소에 도메인을 적용한다.
5. NginX와 도메인을 연결한다.
6. http로 접근시 https로 리다이렉트한다.
7. letsencrypt 에서 Certbot으로 인증서를 발급받는다.
8. Nginx에 적용한다.
9. flask와 Nginx를 연동한다.
10. 완성!

과정이 매우 복잡하였지만 실제 테스트 해본결과 letsencrypt에서 제공하는 인증서가 MacOS에서 문제없이 잘 작동하였다!

### NginX 도메인, flask 연결 코드

/etc/nginx/conf.d에 defalut.conf

![image](https://user-images.githubusercontent.com/62547169/132802009-c8cca4ad-b6de-4374-8b93-c144cd652c2d.png)

/etc/nginx/sties-available에 defalut

![image](https://user-images.githubusercontent.com/62547169/132802286-ed5974cf-ae89-409b-863c-9ee4c41953e2.png)


flask 폴더

test.ini

![image](https://user-images.githubusercontent.com/62547169/132802358-95fef539-019d-4423-b223-c2101f5acdf3.png)

wsgi.py

![image](https://user-images.githubusercontent.com/62547169/132802396-24679c3f-f2e1-428e-81fd-cee72fdd8d3b.png)



끝
