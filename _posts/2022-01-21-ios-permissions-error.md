---
layout: post
title: React Native 권한오류
subtitle: 내 마음대로 권한 오류
categories: React Native
tags: [React Native]
---

react native에 갤러리를 ios에서 들어가야하는데 오류가 생긴다.

그럴 떄는 아래의 항목을 Info.plist에 추가 해보자

```
<dict>
  .
  .
  .
	<key>NSPhotoLibraryUsageDescription</key>
    <string>$(PRODUCT_NAME) would like access to your photo gallery</string>
    <key>NSCameraUsageDescription</key>
    <string>$(PRODUCT_NAME) would like to use your camera</string>
    <key>NSPhotoLibraryAddUsageDescription</key>
 ```
