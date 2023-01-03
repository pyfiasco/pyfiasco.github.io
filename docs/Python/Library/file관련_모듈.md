---
layout: default
title: 파일 관련 모듈
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
import os

for i in ['./ch14/poem.txt', './ch01', '.', '..']:
    p1 = os.path.exists(i)                        # 경로 존재 여부 확인
    print(p1)

f = './ch14/poem.txt'
print(os.path.isfile(f))                           # file 여부 확인
print(os.path.isdir('.'))                          # directory 여부 확인
print(os.path.isabs('./ch14/poem.txt'))            # 절대경로 여부
```
```python
import shutil

shutil.copy('./ch14/poem.txt', './ch14/poem2.txt')  # 파일 복사
shutil.move('./ch14/poem.txt', './ch14/poem2.txt')  # 이동(원본 삭제)

os.rename('./ch14/poem2.txt', './ch14/poem.txt')    # rename

os.chmod('./ch14/poem.txt', 0o400)                  # 읽기 전용으로 전환
import stat
os.chmod('./ch14/poem.txt',stat.S_IRUSR)            # 위와 동일 기능

os.remove('./ch14/poem2.txt')                       # 파일 삭제

os.mkdir('./ch14/new_dir')                          # 디렉터리 생성
result = os.path.exists('./ch14/new_dir')
print(result)

os.rmdir('./ch14/new_dir')                           # 디렉터리 삭제


os.mkdir('./ch14/new_dir')                           # 디렉터리 생성
os.mkdir('./ch14/new_dir/mcintyre')
print(os.listdir('./ch14/new_dir'))                  # 디렉터리 내용을 list화

os.chdir('./ch14/new_dir/mcintyre')                  # 현재 디렉터리 변경
os.mkdir('new')
```
```python
glob()함수관련 문자
- * : all (정규표현식*과 동일)
- ? : 한문자에 일치
- [abc] : a,b,c에 일치
- [!abc] : not a,b,c


import glob
result = glob.glob('./ch14/*.txt')                     # 파일, 경로 찾기
print(result)
```
```python
# 경로 관리
# 파이션의 경로 구분자(기본값): /
# 루트 디렉터리 : 현재 디렉터리


# 경로이름 작성 ( 만들기X )
# /,\사용
# os.path.join()함수 이용
# pathlib 모듈 이용

result = os.path.abspath('test.py')                     #상대경로 -> 절대 경로 변환
print(result)
# C:/Users/neo21/Downloads/introducing-python-master/introducing-python-master/test.py

p = os.path.join('eek','urk','snort.txt')               # 경로 이름 작성
print(p)           



from pathlib import Path
   # 경로 작성
print(file_path)              # ch14 \ urk\ snort.txt
print(type(file_path))        # <class 'pathlib.WindowsPath'>
print(file_path.name, file_path.suffix, file_path.stem) # snort.txt .txt snort

from pathlib import PureWindowsPath,Path
file_path = Path('ch14') / 'urk' / 'snort.txt'
result = PureWindowsPath(file_path)
print(result)         # ch14\urk\snort.txt

```