---
layout: post
title: RestAPI를 사용해 NodeJS에서 Flask로 POST!
subtitle: 웹간의 통신 방식을 간단하게 해보기
categories: ETC
tags: [Web]
---

```
이 예제는 아주 간단하게 테스트를 해보는 예제이다.
```


### NodeJS 샘플코드

```javascript
const axios = require('axios');
axios.post("http://127.0.0.1/todos", { 
	data: "hello",
});
```


### Flask 



