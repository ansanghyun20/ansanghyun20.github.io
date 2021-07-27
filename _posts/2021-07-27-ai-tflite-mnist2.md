---
layout: post
title: 인공지능 - mnist-tflite 모델 생성
subtitle: 인공지능
categories: AI
tags: [AI]
---


### 1. mnist h5 모델 생성

- 바로 tflite를 만들었을 때 사용에 항상 오류가 있었다.
- 그래서 h5를 생성하고 .pb를 생성하고 .tflite로 만든다.

```python
import tensorflow as tf

mnist = tf.keras.datasets.mnist

(x_train, y_train),(x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0

model = tf.keras.models.Sequential([
  tf.keras.layers.Flatten(),
  tf.keras.layers.Dense(512, activation=tf.nn.relu),
  tf.keras.layers.Dropout(0.2),
  tf.keras.layers.Dense(10, activation=tf.nn.softmax)
])

model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

model.fit(x_train, y_train, epochs=10)
model.evaluate(x_test, y_test)

model.save("model.h5")
```

### 2. .pb 생성

- convert

```python
from tensorflow import keras
model = keras.models.load_model('/Users/hyun/Desktop/Study/mask/Train Code(Python)/model.h5', compile=False)

export_path = './pb'
model.save(export_path, save_format="tf")
```


### 3. .tflite 생성

```python
import tensorflow as tf

saved_model_dir = './pb'
converter = tf.lite.TFLiteConverter.from_saved_model(saved_model_dir)
converter.target_spec.supported_ops = [tf.lite.OpsSet.TFLITE_BUILTINS,
                                       tf.lite.OpsSet.SELECT_TF_OPS]
tflite_model = converter.convert()
open('./tf/mnist.tflite', 'wb').write(tflite_model)
```
