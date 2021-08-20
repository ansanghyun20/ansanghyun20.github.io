---
layout: post
title: 인공지능 - mnist를 TensorFlowLite로?
subtitle: 인공지능
categories: AI
tags: [AI]
---

### mnist tflite로 불러와서 사용해보기


#### 1. 모듈 import

```python
import tensorflow as tf
from tensorflow import keras
import numpy as np
import matplotlib.pyplot as plt

print("TensorFlow version {}".format(tf.__version__))
```


#### 2. tesorflow 버전 관리

- python 2.x 버전과 1.x 버전의 차이가 있어서 아래와 같은 코드를 먼저 추가해준다.
- 아래에 차이점을 설명해두었다.

```python
import tensorflow.compat.v1 as tf
tf.disable_v2_behavior()
```

#### 3. 모듈 불러오기 및 모듈 정보 표시

- 우선 파일 path를 지정한다.

```python
tflite_mnist_model = "mnist.tflite"   # 동일한 파일 경로
```

- 경로를 설정하고 정보를 표현한다.

```python
interpreter = tf.compat.v1.lite.Interpreter(model_path=tflite_mnist_model) # 모듈 지정
interpreter.allocate_tensors()

print("== Input details ==")
print("name:", interpreter.get_input_details()[0]['name'])
print("shape:", interpreter.get_input_details()[0]['shape'])
print("type:", interpreter.get_input_details()[0]['dtype'])

print("\n== Output details ==")
print("name:", interpreter.get_output_details()[0]['name'])
print("shape:", interpreter.get_output_details()[0]['shape'])
print("type:", interpreter.get_output_details()[0]['dtype'])

print("\nDUMP INPUT")
print(interpreter.get_input_details()[0])
print("\nDUMP OUTPUT")
print(interpreter.get_output_details()[0])
```

#### 테스트 

```python
from PIL import Image
import PIL.ImageOps    

img = Image.open("test.png").convert('L').  # 직접 만든 Test image
img.load()
img = PIL.ImageOps.invert(img)
data = np.asarray( img, dtype="int32" )

plt.grid(False)
plt.xticks([])
plt.yticks([])
plt.imshow(data, cmap=plt.cm.binary)

data = data / 255.0
inputImg = np.expand_dims(data,0).astype(np.float32)
inputImg.shape

input_details = interpreter.get_input_details()
interpreter.set_tensor(input_details[0]['index'], inputImg)

interpreter.invoke()

output_details = interpreter.get_output_details()
output_data = interpreter.get_tensor(output_details[0]['index'])
print("Prediction results:", output_data)
print("Predicted value:", np.argmax(output_data))
```

<img width="700" alt="image" src="https://user-images.githubusercontent.com/62547169/127098334-b15688a2-a6b7-4b52-94be-714418cf2126.png">
