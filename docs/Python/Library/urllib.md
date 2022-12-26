---
layout: default
title: urllib
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

```python
import urllib.request
from urllib import request,error, parse, robotparser


url = "http://www.daum.net"

# site 읽기
# urllib.request.urlopen(url, data=None, [timeout, ]*, cafile=None, capath=None, cadefault=False, context=None)
response_obj = urllib.request.urlopen(url)
print(response_obj)   # <http.client.HTTPResponse object at 0x000001DCAB8AFF70>
read_obj = response_obj.read()  # read object 생성
print(read_obj.decode('utf-8'))   # decode적용

# site 상태 확인
status = response_obj.status
print(status)


# 이미지 검색/저장
try:
    url = r"https://t1.daumcdn.net/news/202212/23/newsis/20221223091113153rsaf.jpg"
    response_obj2 = urllib.request.urlopen(url)
    read_obj = response_obj2.read()
    filename = "picture1.jpg"
    # wb는 Write Binary
    with open(filename, mode="wb") as f:
        #메모리의 이미지를 파일로 저장
        f.write(read_obj)
        f.close()
        print("저장완료!!")
except:
    pass


url = "https://www.naver.com"
try:
    read_obj = urllib.request.urlopen(url).read()
    print(read_obj.decode('utf-8'))
except :
    pass

# url parse
site = r"https://예시도메인/articles/2?test=hanpy&key=abcd"
parsing = urllib.parse.urlparse(site)
print (parsing)       # ParseResult(scheme='https', netloc='예시도메인', path='/articles/2', params='', query='test=hanpy&key=abcd', fragment='')
q = parsing.query     # query 값 반환
print(q)

return_result = urllib.parse.parse_qs(q)
print(return_result)


# 인코딩처리 - 공백을 처리하는 방식 :   + (quote_plus함수) / %20 (quote함수)
print('파이썬은 hanpy')                          # 파이썬은 hanpy
print(urllib.parse.quote('파이썬은 hanpy'))      # %ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%9D%80%20hanpy
print(urllib.parse.quote_plus('파이썬은 hanpy')) # %ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%9D%80+hanpy
```