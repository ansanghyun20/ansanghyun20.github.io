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

여기서 Flask 에서 OpenSSL을 사용하지 않아도 되고 Nginx에서 바로 https를 적용해 Flask서버 또한 https에 접속 완료!





### Flask 소스 코드

```python


import numpy as np
import time
import tensorflow as tf
import ssl
from flask_cors import CORS
from tensorflow.keras.models import load_model # 인공지능 관련 라이브러리

from flask import Flask, request
from flask_restx import Resource, Api # flask 서버 관련 라이브러리

import threading

model = load_model('model.h5') # 포즈 추정모델을 사용하기 위함
app = Flask(__name__)
api = Api(app)

CORS(app)

todos = {}
count = 1
result = {}



@api.route('/todos')
class TodoPost(Resource):
    def post(self):
        global count
        global todos
        global result
        idx = count
        count += 1

        exercise = request.json.get('kind')
        print("ExerciseKind:", exercise)
        if exercise == "kind_squat":
        # Rest API 가져오기
            name = request.json.get('name')
            postData = request.json.get('data')

            reshapeData = np.array(list(map(int,postData)))
            modelPredict = model.predict(np.reshape(reshapeData, (1,2,14)))
            if list(modelPredict[0]).index(max(modelPredict[0])) == 0:
                result[name] = "Stand"
            elif list(modelPredict[0]).index(max(modelPredict[0])) == 1:
                result[name] = "Squat"
            elif list(modelPredict[0]).index(max(modelPredict[0]))==2:
                result[name] = "Bent"
            print(result)

        return {
            'name': name,
            'data': postData
        }


@api.route('/todos/result')
class TodoSimple(Resource):
    def get(self):
        return {
            'AllData': result,
        }

    def put(self, todo_id):
        todos[todo_id] = request.json.get('data')
        return {
            'todo_id': todo_id,
            'data': todos[todo_id]
        }

    def delete(self, todo_id):
        del todos[todo_id]
        return {
            "delete" : "success"
        }

if __name__ == "__main__":
 #   ssl_context = ssl.SSLContext(ssl.PROTOCOL_TLS)                                                           //openSSL을 적용했던 흔적
#    ssl_context.load_cert_chain(certfile='cert.pem', keyfile='key.pem')
    app.run(debug=True, host='IP' ,port = 포트 ) #, ssl_context=ssl_context)


```







### Nginx 세팅


conf.d -> default.conf

```

server {
    listen       80;
    server_name  도메인주소;

    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;

    location / {
        return 307 https://도메인주소$request_uri;
    }
}

server {
        listen 443;
        listen [::]:443;
        ssl on;
        server_name 도메인주소;

        ssl_certificate /etc/letsencrypt/live/도메인주소/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/도메인주소/privkey.pem;

        location / {
                include proxy_params;
                proxy_pass flask주소;
        }
}


```


site-available


```
server {
         listen 443 ssl default_server;
         listen [::]:443 ssl default_server;

        ssl on;
        server_name 도메인주소;

        location / {
                add_header 'Access-Control-Allow-Orgin' '*';
                try_files $uri @app;
        }

        location @app {
                include uwsgi_params;
                uwsgi_pass unix: test.sock 경로;
        }
        ssl_certificate /etc/letsencrypt/live/도메인주소/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/도메인주소/privkey.pem;

}


server{
        server_name 도메인주소;
        listen 80;
        location / {
                return 307 https://도메인주소$request_uri;
        }
}


```
