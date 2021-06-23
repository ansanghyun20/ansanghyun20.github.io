---
layout: post
title: BeautifulSoup
subtitle: BeautifulSoup
categories: python
tags: [beautifulsoup]
sidebar: []
---

이 라이브러리는 웹 크롤링을 하기 위해서 사용됩니다.

### BeautifulSoup 설치하는 방법

pip shell command를 이용합니다.

```cmd
% pip install beautifulsoup4
```

### BeautifulSoup 간단한 예제

beautifulsoup.py

```python

import requests
from bs4 import BeautifulSoup     # module import

url = 'Web Site URL'

resp = requests.get(url)

if resp.status_code == 200:
        html = resp.text
        soup = BeautifulSoup(html, 'html.parser')
        print(soup)
else :
        print(resp.status_code)

# make html file

fi = open("a.html","w")
fi.write(str(soup))
fi.close()

```

실행 및 결과

![image](https://user-images.githubusercontent.com/62547169/123041036-bb8c0800-d42f-11eb-8627-ab27c77c2505.png)

파일을 실행해서 결과를 확인할 수 있고 내용을 확인할 수 있습니다.


### select 검색

find 보다 속도가 빠르고 직관적이다.


- id            ->              `#id명             or      태그#id명`
- class         ->              `.class명          or      태그.class명`

-` 태그 > 자식태그`     ->      바로 아래 태그
- `태그  자손태그`     ->      아래의 모든 태그


```python

import requests
from bs4 import BeautifulSoup     # module import

soup = BeautifulSoup(open(r'/Users/hyun/Desktop/shopping/shopping.html'), 'html.parser')

print(soup.select('태그 이름 입력'))


```

