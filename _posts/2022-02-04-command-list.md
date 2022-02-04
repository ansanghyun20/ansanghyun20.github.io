---
layout: post
title: Dockerfile 명령어 List - 2 !
subtitle: 도커를 공부해보자
categories: Docker
tags: [Docker]
---

### Dockerfile 학습 명령어 List

Dockerfile에 들어가는 명령어 정리

#### FROM

Docker에서 Base Image를 결정한다. 

```Dockerfile

FROM ubuntu:VERSION  # centos~
.
.
.

```

#### RUN

Docker내부에서 실행되는 명령어

```Dockerfile

RUN apt-get update
RUN apt-get install -y nginx
RUN echo "~~~"

```

#### WORKDIR

작업 디렉토리 설정

CMD 명령어가 실행될 경로 설정

```Dockerfile

WORKDIR /etc/nginx

```

#### CMD

명령어 사용

--------------------------------------------------------
2. build-arg
3. VOLUME
4. EXPOSE
6. ENTRYPOINT
