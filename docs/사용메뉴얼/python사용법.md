---
layout: default
title: python 사용법

parent: 사용메뉴얼
has_children: true
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## python 설치 관련
```python
$ pip install flask
$ pip install flask==0.9.0   # 버전지정
$ pip install 'flask≥0.9.0'  # 최소버전 지정
$ pip -r requirements.txt    # requirements.txt파일을 이용한 설치
$pip install --upgrade flask # upgrade
$pip uninstall flask         # 패키지 삭제
$python -V                   # 버전 확인
```

## pip / 모듈
- pip명령어 위치: C:\Users\neo21\AppData\Local\Programs\Python\Python311\Scripts\pip.exe
- 사용자 환경변수 등록/변경(pip.exe위치 등록)
    - C:\Users\neo21\AppData\Local\Programs\Python\Python311\Scripts 
- 모듈 설치 
    1. pip명령어 위치로 이동
    2. pip install <모듈명>
    3. 모듈 설치 위치: C:\Users\neo21\AppData\Local\Programs\Python\Python311\Lib\site-packages