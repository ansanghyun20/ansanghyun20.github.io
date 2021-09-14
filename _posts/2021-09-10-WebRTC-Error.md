---
layout: post
title: WebRTC 시행착오 정리
subtitle: WebRTC 시행착오
categories: JavaScript
tags: [Web]
---

## WebRTC 

WebRTC는 서버를 거치지 않고 사용자끼리 영상을 연결해주는 기술이다.

유튜브의 zoomclone을 치면 나오는 예제를 사용했다.

예제는 http 환경에서 열리고 여기서 `LocalTunner, Ngrok등을 사용했는데 문제가 생겼다.`

1. 연결이 잘되는 환경이 있고 안되는 환경이 많다.
2. 학교 강의실와이파이로는 대체로 안됐다. 
3. 개인 집 환경에서는 잘됐었지만 서로서로 잘 안보이고 누구는 보이고 누구는 안보이는 경우가 생겼다.

이를 위해서 아래의 개념들을 공부를 해봤다.

### Sturn? Turn? 개념??

아직 Sturn과 turn의 개념에 대해 정확히 알지 못했다.

현재 WebRTC를 쓰는 프로젝트를 진행중인데 Ubuntu로 Coturn을 설치해 테스트를 해봤는데 전혀 동작하지 않았다.

따라서 다른 turn서버를 제공해주는 링크를 사용하였다.

구글에 `public sturn server`를 치면 많이 나오는 것 같다.

그래도 이걸로 해결 된건 아니다.

### 그래서 어떻게 해결?

`LocalTunner, Ngrok로 https 환경을 만들어 주는 것이 문제였다.`

그래서 `NodeJS에서 바로 OpenSSL`을 적용할 수 있는 환경을 만들어 주었다.

통신이 생각보다 매끄럽게 이전보다 잘 됐다.

테스트를 많이 해본 것은 아니지만 이전 보다는 확실히 개선 됐다.

끝

### 9/14 추가

끝 인줄 알았으나 또 다른 문제가 생겼다.

OpenSSL을 사용하니 이것또한 적용이 되는 인터넷 환경, 적용이 안되는 인터넷 환경이 생겼다.

Nginx 시행착오처럼 Letsencrypt를 적용해보자.



