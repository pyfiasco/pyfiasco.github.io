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

## os모듈


```python
# 경로 존재 여부 확인

import os
for i in ['./ch14/poem.txt', './ch01', '.', '..']:
    p1 = os.path.exists(i)                        
    print(p1)

# file형식, directory형식,절대경로형식 여부 확인
f = './ch14/poem.txt'
print(os.path.isfile(f))                           # file 여부 확인
print(os.path.isdir('.'))                          # directory 여부 확인
print(os.path.isabs('./ch14/poem.txt'))            # 절대경로 여부
```

```python
# shutil 모둘을 이용한 copy, move
import shutil
shutil.copy('./ch14/poem.txt', './ch14/poem2.txt')  # 파일 복사
shutil.move('./ch14/poem.txt', './ch14/poem2.txt')  # 이동(원본 삭제)
```

```python
# 다른 os모듈 함수 - rename / 파일 삭제 / 읽기 전용으로 전환 
os.rename('./ch14/poem2.txt', './ch14/poem.txt')    # rename
os.remove('./ch14/poem2.txt')                       # 파일 삭제

os.chmod('./ch14/poem.txt', 0o400)                  # 읽기 전용으로 전환
import stat
os.chmod('./ch14/poem.txt',stat.S_IRUSR)            # 위와 동일 기능
```

```python
# 디렉터리 생성-삭제 / 현재디렉터리 변경
result = os.path.exists('./ch14/new_dir')
if result == False:
    os.mkdir('./ch14/new_dir')                       # 디렉터리 생성
os.rmdir('./ch14/new_dir')                           # (빈)디렉터리 삭제
print(os.listdir('./ch14/new_dir'))                  # 디렉터리 내용을 list화
os.chdir('./ch14/new_dir/mcintyre')                  # 현재 디렉터리 변경
```


glob()함수관련 문자
- * : all (정규표현식*과 동일)
- ? : 한문자에 일치
- [abc] : a,b,c에 일치
- [!abc] : not a,b,c


```python
# 파일, 경로 찾기
import glob
result = glob.glob('./ch14/*.txt')                     
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
```

```python
# 경로 작성
from pathlib import Path
print(file_path)              # ch14 \ urk\ snort.txt
print(type(file_path))        # <class 'pathlib.WindowsPath'>
print(file_path.name, file_path.suffix, file_path.stem) # snort.txt .txt snort

from pathlib import PureWindowsPath,Path
file_path = Path('ch14') / 'urk' / 'snort.txt'
result = PureWindowsPath(file_path)
print(result)         # ch14\urk\snort.txt
```

## pathlib모듈

[참조](https://m.blog.naver.com/hankrah/221843966812)

os.path 와 Pathlib의 가장 큰 차이점은, 경로를 문자열로 다루냐, 객체로 다루냐 차이


### 절대 경로 반환 : path(경로/파일)

```python 
### Get a path to the current Python file
import pathlib
curr_file = pathlib.Path(__file__)
print(curr_file)
``` 
- Jupyter 노트북에서 __file__ 속성에 액세스할 수 없으므로 작동하지 않습니다. 


#### 현재 작업 디렉토리의 경로 반환 : cwd()

```python
cwd = pathlib.Path.cwd()
print(cwd)
```
- home() 
사용자의 홈 디렉토리를 가리키는 새 경로를 반환합니다(os.path.expanduser('~')에 의해 반환됨).


#### 현재 작업 디렉터리의 상위 디렉터리 반환 : parent 속성

```python
one_above = pathlib.Path.cwd().parent 
print(one_above)
```

#### N 번째 상위 폴더 경로 반환 : parents[index]

```python
### 2번째 상위폴더 반환
mul_above = pathlib.Path.cwd().parent.parent
mul_above = pathlib.Path.cwd().
print(mul_above)
```

### Join paths : joinpath(파일/경로)

```python
tgt_fname = 'summer-sales.csv'
print(mul_above.joinpath(tgt_fname))
```

### 존재하지 않는 경우 디렉토리 만들기 : mkdir()

exists() 를 사용하여 폴더가 이미 존재하는지 확인 후 mkdir() 를 사용하여 폴더 생성 <- 존재하는 디렉터리 생성 시 에러 발생

```python
tgt_path = pathlib.Path.cwd().joinpath('reports')
if not tgt_path.exists():
    tgt_path.mkdir()
```
### 빈 디렉터리 삭제 : rmdir()
이 디렉터리를 제거합니다.  디렉터리는 비어 있어야 합니다.

- rename(self, target)
이 경로의 이름을 대상 경로로 바꿉니다.
 
- replace(self, target)
이 경로의 이름을 대상 경로로 바꾸고 해당 경로가 있으면 덮어씁니다.


### 폴더의 파일/폴더 반복 : iterdir() 

```python
tgt_path = pathlib.Path.cwd()
for file in tgt_path.iterdir():
    print(file)
```

### 폴더의 파일/폴더 반복 : glob(pattern)
이 하위 트리를 반복하고 모든 기존 파일 (디렉토리를 포함한 kind)가 주어진 상대 패턴과 일치합니다.
generator object 생성

```python
tgt_path = pathlib.Path.cwd()
for file in tgt_path.glob('*.py'):
    print(file)
```

### 파일 만들기 : touch(exist_ok=True)

```python
tgt_path = pathlib.Path.cwd().joinpath('reports')
tgt_path.joinpath('summer-sales.csv').touch(exist_ok=True)
tgt_path.joinpath('winter-sales.txt').touch(exist_ok=True)
exist_ok=True 파라미터는 파일이 이미 존재하는 경우 파일을 덮어쓰도록 파이썬에 지시합니다.
```

### path가 폴더인지 확인 : is_dir() - bool 반환
### path가 파일인지 확인 : is_file() - bool 반환

```python
tgt_path = pathlib.Path.cwd().joinpath('reports')
print(tgt_path.is_dir())
print(tgt_path.joinpath('summer-sales.csv').is_dir())
```

### path 마지막 요소의 이름 반환 : name 속성

```python
tgt_path = pathlib.Path.cwd().joinpath('summer-sales.csv')
print(tgt_path.name)
```

### path 마지막 요소의 확장자 반환 : suffix 속성

```python
tgt_path = pathlib.Path.cwd().joinpath('reports/summer-sales.csv')
print(tgt_path.suffix)
```
- 디렉터리는 ''반환

### path 마지막 요소의 stem 반환 : stem 속성
마지막 경로 구성 요소에서 마지막 접미사를 뺀 값입니다.
- 파일 : 확장자를 제외한 파일명
- 디렉터리 : 폴더명


## 기타
- open(self, mode='r', buffering=-1, encoding=None, errors=None, newline=None)
이 경로가 가리키는 파일을 열고 내장 open() 함수처럼 파일 객체를 반환합니다.
- read_bytes(self)
파일을 바이트 모드로 열고 읽은 다음 파일을 닫습니다.
- read_text(self, encoding=None, errors=None)
텍스트 모드에서 파일을 열고 읽은 다음 파일을 닫습니다.
- write_bytes(self, data)
파일을 바이트 모드로 열고 쓴 다음 파일을 닫습니다.
- write_text(self, data, encoding=None, errors=None, newline=None)
텍스트 모드에서 파일을 열고 쓴 다음 파일을 닫습니다.










