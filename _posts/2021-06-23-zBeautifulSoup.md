---
layout: post
title: BeautifulSoup
subtitle: BeautifulSoup
categories: python
tags: [beautifulsoup]
sidebar: []
---

This library is used for web crawling.

### How to install BeautifulSoup

pip shell command

```cmd
% pip install beautifulsoup
```

### A brief example of BeautifulSoup

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

Run and Result

![image](https://user-images.githubusercontent.com/62547169/123040643-0f4a2180-d42f-11eb-896e-6801edfb3a2f.png)


