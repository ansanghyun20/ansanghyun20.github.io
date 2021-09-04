---
layout: post
title: IITP_F - https와 http에 대한 사건(렛츠인크립트)
subtitle: 이야기
categories: Project
tags: [Web]
---

### 사건 발단

Node JS(WebRTC 및 포즈 추정) <-> Flask(AI Server) Axios통신중 문제

Node JS(local tunnel)사용

Flask(OpenSSL로 https)

Axios를 사용하는 이유 : 추정된 포즈값을 인공지능 서버로 보내기 위함

1. Rest API를 Axios로 사용하던 중에 http를 통신하는데 전혀 문제가 되지 않았음
2. WebRTC를 사용하기위해서는 https를 사용해야했고 그 속에서 Axios를 사용하기 위해서 https환경에서 해야했음
3. https통신을 처음에는 Flask(AI server)에 OpenSSL인증서를 설치해 바로 통신
4. 여기서 `문제점`은 Mac OS 또는 Windosw 환경에서 인증서가 제대로 작동 되지 않는 곳이면 Axios 통신이 굉장히 불안정 했고 오류가 많이남
5. `또한 Flask에 바로 SSL 인증서를 올려서 사용하지 않는 점 또한 알게 됨`


### 해결법

1. nginx를 사용해 Flask를 라우팅하고
2. 도메인을 발급 받아 렛츠 인크립트를 사용하는 방법을 도전
3. GoDaddy에서 우리의 팀명인 www.zaba.website 를 발급
4. https://IP 이주소로 마스크 및 할당 (80포트 기본사용)
5. 렛츠인크립트를 위 도메인주소로 암호화 (.pem 등) 발급
6. nginx에서 렛츠인크립트 설정 및 80포트를 사용했을경우 443으로 넘겨줌
7. 따라서 아래와 같은 통신을 하게됨

수정 전 : Node JS(local tunnel)          <->          Flask(AI Server)

수정 후 : Node JS(local tunnel) <->     Nginx     <-> Flask(AI Server)
