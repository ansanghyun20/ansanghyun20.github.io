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
axios.post("http://127.0.0.1:5000/hello", { 
	data: "hello",
});
```


### Flask 샘플코드

```python

from flask import Flask, request
from flask_restx import Resource, Api # flask 서버 관련 라이브러리

app = Flask(__name__)
api = Api(app)

data = {}
count = 1

@api.route('/hello')
class TodoPost(Resource):
    def post(self):
        global count
        global data
        
        index = count
        count += 1
        data[index] = request.json.get('data')

        return {
            'index': index,
            'data': data[index]
        }


if __name__ == "__main__":
    app.run(debug=True, host='0.0.0.0', port=5000)


```



