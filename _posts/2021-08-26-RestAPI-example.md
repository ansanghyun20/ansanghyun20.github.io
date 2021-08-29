---
layout: post
title: RestAPI를 사용해 NodeJS에서 Flask로 POST!
subtitle: 웹간의 통신 방식을 간단하게 해보기
categories: ETC
tags: [Web]
---

```
이 예제는 아주 간단하게 테스트를 해보는 예제이다.
이 코드는 http://127.0.0.1:5000/hello에 js에 적힌 data값을 flask로 전송한다.
flask에서는 Post를 받아 data 딕셔너리에 값이 저장되는 코드이다. 
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


### 사용방법

1. 우선 flask 서버를 실행한다.
2. 그 후에 NodeJS코드를 실행해 본다.

 
3. 전송

![image](https://user-images.githubusercontent.com/62547169/130900678-53880194-42c2-45b1-b093-e6f7cb7c1887.png)



4 . 확인


![image](https://user-images.githubusercontent.com/62547169/130900743-98334ead-99e1-4720-981b-b30e254d4586.png)


