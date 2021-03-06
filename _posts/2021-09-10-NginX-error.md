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

![image](https://user-images.githubusercontent.com/62547169/132802596-d680b913-88dd-4b5a-8f7a-8b1bdfdd58f8.png)

wsgi.py

![image](https://user-images.githubusercontent.com/62547169/132802396-24679c3f-f2e1-428e-81fd-cee72fdd8d3b.png)



끝


### 9월 14 추가

끝인줄 알았으나 Clinet(NodeJS) <-> Server(Flask) 통신에서 오류가 났다.

Axious 요청을 잘 하다가도 `인증서의 이름이 일치하지 않는다는 내용을 발견`했다.

1. NodeJS 에는 OpenSSL을 적용했다. (테스트 용도)
2. Flask 에는 Letsencrypt를 적용했다.
3. 여기서 인증서가 겹치는 오류가 발생할 수 있다는 가정


위에 것이 오류가 날 수 있다는 가정 1

1. Godaddy에서 도메인 설정을 (원하는 주소로)전달 쪽에서 했다.
2. 전달부분을 지우고(아이피 설정 부분에 이상한 아이피가 지워졌다.) 도메인 설정에서 바로 넣었다.
3. 전달 부분에서 Goddady 측의 https 인증서가 오류를 낸 것 같다.

이것은 가정 2다.

개인적으로 가정 2의 말이 더 맞는 것 같다.

문제는 가정1, 가정2를 다 해결해서 사라졌다.
