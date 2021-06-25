---
layout: post
title: Swift Syudy! - 1
subtitle: Swift
categories: swift
tags: [swift]
---

```
자바를 통해서 안드로이드 앱을 개발해 본 적이 있다.
앱 개발한 경험이 너무 재미있었어서 아이폰 앱을 개발해보는 것 또한 재밌을 것 같아서 도전 해본다.
스위프트의 기초적인 문법부터 알아간다.
```

맥의 PlayGround앱을 사용하는데 화면은 아래와 같다.

![image](https://user-images.githubusercontent.com/62547169/123423570-aca58100-d5fa-11eb-9c46-a8f05a06d9cd.png)


### 변수

변수 작성 규칙은 다음과 같다. 주의사항은 주석에!

출력은 파이썬과 비슷하게 print를 쓰면 된다.


```swift

// 1. var 변수명 = 값
// 2. var 변수명 : 타입 = 값
// 띄어쓰기 준수, 타입 대문자 준수
// int(x) , Int(o)

var v1 = 123
var v2 : Int = 123

print(v1)
print(v2)

```

#### 종류

많은 종류가 올 수 있지만 기본적인 종류는 아래와 같다.

```
Bool
String
Int
Double
Float
```




### 상수

상수는 한 번 정의하면 바꿀 수 없는 수 이다.

아래와 같이 선언한다.

```swift

let v = 123
print(v)

v = 456     // 오류

```

상수를 미리 정의해놓고 쓰는 방법도 있다.

```swift

let v : Int
v = 123

print(v)

```


### 배열

Swift에서 배열을 쓰는 방법은 다양한 것 같다.

기본적으로 쓰는 방법은 자바의 제네릭같이 생긴 것도 쓴다.

```swift

var arr : Array<Int> = [1,2,3]
print(arr)

// 아래와 같이 사용할 수 있는데 나는 안쓸거같다.
var arr2 : Array<Int> = Array<Int>(arrayLiteral: 1,2,3)
print(arr2)

```


위와같이 
위와같이 표
