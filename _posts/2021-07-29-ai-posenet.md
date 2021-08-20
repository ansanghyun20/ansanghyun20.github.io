---
layout: post
title: PoseNet을 사용해서 포즈 추정하기
subtitle: 포즈 추정하는 방법
categories: AI
tags: [AI]
---

### 순서와 방법

1. PoseNet 라이브러리로 nose, left eye, right eye 등을 출력해본다.
2. 출력된 결과물을 CSV 형태로 저장한다.
3. SKlearn을 사용해 CSV파일을 불러와 학습을 진행한다.
4. 모델을 예측한다.

### PoseNet 라이브러리

* https://github.com/rwightman/posenet-python


### 8/20 추가

PoseNet 라이브러리성능이 그닥 좋은 방법이 아닌거같다. 따라서 앞으로는 Mediapipe의 포즈 추정을 사용하는 방법을 공부한다.




