---
layout: post
title: IITP_F - 자바스크립트로 Mediapipe를 돌리고 원하는 좌표를 출력
subtitle: 포즈 추정하는 방법
categories: Project
tags: [Web]
---


### 자바 스크립트 코드


![image](https://user-images.githubusercontent.com/62547169/130901593-e7bb7460-6b6f-45fe-992b-b7884f935a8e.png)




mediapipe의 0 ~ 10번까지, 15 ~ 22번까지는 우리가 사용하는 포즈 추정에서 필요없는 부분이라서 제외했다.
아래와 같이 poseLandmarks를 이용하면 포즈를 인식한 딕셔너리를 가질 수 있게 되는데 이것을 사용하는 형식에 맞게 정하면 된다.

```javascript
  var arr = []; //배열을 명시 해야함
  var i;
  var tempX;
  var tempY;
  for (i = 11; i < results.poseLandmarks.length; i++) {
    //console.log('Walking east one step'+i);
    if(i==15 || i==16 || i==17 || i==18 || i==19 || i==20 || i==21 || i==22){
                continue;
    }
    else{
      tempX = results.poseLandmarks[i]["x"]*1280;
      tempY = results.poseLandmarks[i]["y"]*720;
      arr.push(tempX)
      arr.push(tempY)
       console.log("hello"+JSON.stringify(results.poseLandmarks[i]["y"])*960);

      //console.log("Y:"+tempY);
      //arr.push(results.poseLandmarks[i]["x"]*1280+results.poseLandmarks[i]["y"]*720);
    }
  }

```



