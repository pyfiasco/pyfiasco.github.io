---
layout: default
title: sys
parent: Library
grand_parent: Python
---

# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 검색 모듈 path 확인 : sys.path
```python
import sys

for i in sys.path:
    print(i)

"""
c:\Users\neo21\Downloads\introducing-python-master\introducing-python-master
C:\Users\neo21\AppData\Local\Programs\Python\Python311\python311.zip
C:\Users\neo21\AppData\Local\Programs\Python\Python311\Lib
C:\Users\neo21\AppData\Local\Programs\Python\Python311\DLLs
C:\Users\neo21\AppData\Local\Programs\Python\Python311
C:\Users\neo21\AppData\Local\Programs\Python\Python311\Lib\site-packages
"""
```

## 모듈 경로 추가 : sys.insert(index,path)
```python
import sys

sys.path.insert(
    0,
    "C:/Users/neo21/Downloads/introducing-python-master/introducing-python-master/ch11/choices"
)

import advice
print(advice.give())
```