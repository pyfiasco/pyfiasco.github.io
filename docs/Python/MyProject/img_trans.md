---
layout: default
title: PIL이용 image 변환
parent: MyProject
grand_parent: Python
nav_order: 1
---

# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## 이미지 파일 변환 프로그램 완성

```
png -> byte data -> io.BytesIO -> PIL -> save
[link](https://myohyun.tistory.com/218)
```

```python



from PIL import Image
import os
import pathlib
import time
import shutil


def is_path_exists(source_path: str) -> bool:
    path = pathlib.Path(source_path)
    if path.exists():
        return True
    else:
        print("존재하는 경로 / 파일명을 입력하세요")
        return False


def is_dir(source_path: str) -> ['None', 'file', 'directory']:
    path = pathlib.Path(source_path)
    dot_image = ['.' + i for i in image_file]
    L = []

    if path.is_file():
        if path.suffix in dot_image:
            L.append(path)
            print(path.name)
    else:
        for k in path.iterdir():
            if k.is_file():
                if k.suffix in dot_image:
                    L.append(k)
                    print(k.name)
            else:
                for m in k.iterdir():
                    if m.is_file():
                        if m.suffix in dot_image:
                            L.append(m)
                            print(m.name)
    return L


def make_dir(path):
    d = pathlib.Path(path)
    cur = d.cwd()
    c = cur.stem
    try:
        cur.joinpath(c + '_copy').mkdir()
    except:
        pass
    p = cur.joinpath(c + '_copy')
    return (d, p)


def rename(path, prefix):
    path = path
    suffix = path[0].suffix
    target = str(path[1]) + '\\' + prefix + '.' + suffix
    shutil.copy(path[0], target)


def trans_img_to_PIL(img_file_name):
    """image file <name>  -> PIL object"""
    img = Image.open(img_file_name).convert('RGB')
    return img


def trans_PIL_to_img(PIL, new_name):
    PIL.save(new_name)




if __name__ == '__main__':
    image_file = {'png', 'gif', 'jpg', 'jpeg'}
    work_list = None
    while True:
        p = input("경로/파일을 선택 :")
        source_path = pathlib.Path(p)

        if not is_path_exists(source_path):
            continue
        else:
            work_type = is_dir(source_path)  # [ 'None', 'file', 'directory' ]
            if work_type == []:
                print("이미지 파일이 존재하지 않습니다.")
                continue
            else:
                work_list = work_type

        while True:
            select_work = input("""
[작업 선택]
1. change format
2. rename
3. crop
4. resize
0. exit
### 작업 결과는 하위폴더 [복사본]에 저장됩니다.
""")
            if select_work not in ['1', '2', '3', '4']:
                break
            else:
                while True:
                    fmt = input("""    
파일형식을 지정하세요
[ 1:png 2:jpeg 3:jpg 4:gif ] :
""")
                    if fmt not in ['1', '2', '3', '4']:
                        continue

                    L = []
                    format = {'1': 'png', '2': 'jpeg', '3': 'jpg', '4': 'gif'}
                    for i in work_list:
                        L.append(make_dir(i))

                    if select_work == '1':
                        for i in L:
                            r = trans_img_to_PIL(i[0])
                            trans_PIL_to_img(r, str(i[1]) + '\\' + i[0].stem + '.' + format[fmt])
                    elif select_work == '2':
                        prefix = input("prefix를 입력하세요 :")
                        for num, p_ in enumerate(L):
                            suffix = p_[0].suffix
                            target = str(p_[1]) + '\\' + prefix + str(num) + '.' + suffix
                            shutil.copy(p_[0], target)

                    elif select_work == '3':
                        print("기존 파일형식을 유지합니다.")
                        position = int(input('자를 위치 선택 [왼쪽:1 오른쪽: 2] :'))
                        w = int(input("자를 폭 선택 [W] :"))
                        for i in L:
                            r = trans_img_to_PIL(i[0])
                            if w >= r.size[0] or w >= r.size[1]:
                                print("%s보다 작은 폭을 선택하세요" % (max(r.size[0], r.size[1])))
                            else:
                                f = (i[0].suffix)
                                print(f)
                                if position == 1:
                                    c1 = r.crop((w, w, r.size[0], r.size[1]))
                                    trans_PIL_to_img(c1, str(i[1]) + '\\' + i[0].stem + f)
                                    print('done')
                                else:
                                    c1 = r.crop((0, 0, r.size[0] - w, r.size[1] - w))
                                    trans_PIL_to_img(c1, str(i[1]) + '\\' + i[0].stem + f)

                    elif select_work == '4':
                        width = int(input("이미지 size 입력 넓이[W] :"))
                        height = int(input("이미지 size 입력 높이[H] :"))
                        for i in L:
                            r = trans_img_to_PIL(i[0])
                            result = r.resize((width, height))
                            trans_PIL_to_img(result, str(i[1]) + '\\' + i[0].stem + '.' + format[fmt])

                    break

        exit()

```



## BytesIO이용 이미지 파일 변환

```python
### 메모리데이터에서 포맷 변경하기

from PIL import Image
import pathlib
import shutil
from io import BytesIO


def is_path_exists(source_path: str) -> bool:
    path = pathlib.Path(source_path)
    if path.exists():
        return True
    else:
        print("존재하는 경로 / 파일명을 입력하세요")
        return False


def is_dir(source_path: str) -> ['None', 'file', 'directory']:
    path = pathlib.Path(source_path)
    dot_image = ['.' + i for i in image_file]
    L = []

    if path.is_file():
        if path.suffix in dot_image:
            L.append(path)
            print(path.name)
    else:
        for k in path.iterdir():
            if k.is_file():
                if k.suffix in dot_image:
                    L.append(k)
                    print(k.name)
            else:
                for m in k.iterdir():
                    if m.is_file():
                        if m.suffix in dot_image:
                            L.append(m)
                            print(m.name)
    return L


def make_dir(path):
    d = pathlib.Path(path)
    cur = d.cwd()
    c = cur.stem
    try:
        cur.joinpath(c + '_copy').mkdir()
    except:
        pass
    p = cur.joinpath(c + '_copy')
    return (d, p)


def rename(path, prefix):
    path = path
    suffix = path[0].suffix
    target = str(path[1]) + '\\' + prefix + '.' + suffix
    shutil.copy(path[0], target)


def trans_img_to_PIL(img_file_name):
    """image file <img_file_name>  -> PIL object"""
    img = Image.open(img_file_name).convert('RGB')
    return img

def img_to_memory(img_file_name):
    """image file <img_file_name>  -> data"""
    img = Image.open(img_file_name)                                 # .convert('RGB')
    return PIL_to_memory(img)

def trans_PIL_to_img(PIL, new_name):
    PIL.save(new_name)


def PIL_to_memory(PIL, fmt=None):
    """Return image data from PIL Image <PIL>, in <fmt> format"""
    fp = BytesIO()
    if not fmt:
        fmt = PIL.format  # keeps the original format
        PIL.save(fp, fmt)  # writes to memory
    return fp.getvalue()


def memory_to_PIL(data):
    """Return PIL Image object, with data from in-memory <data>"""
    # open함수와 비슷한 기능
    fp = BytesIO(data)
    return Image.open(fp)  # reads from memory


def convert_image(data, fmt=None):
    """Convert image <data> to PIL <fmt> image data  - 포멧 설정"""
    PIL = memory_to_PIL(data)
    return PIL_to_memory(PIL, fmt)

'''
if __name__ == '__main__':
    image_file = {'png', 'gif', 'jpg', 'jpeg'}
    work_list = None
    while True:
        p = input("경로/파일을 선택 :")
        source_path = pathlib.Path(p)

        if not is_path_exists(source_path):
            continue
        else:
            work_type = is_dir(source_path)  # [ 'None', 'file', 'directory' ]
            if work_type == []:
                print("이미지 파일이 존재하지 않습니다.")
                continue
            else:
                work_list = work_type

        while True:
            select_work = input("""
[작업 선택]
1. change format
2. rename
3. crop
4. resize
0. exit
### 작업 결과는 하위폴더 [복사본]에 저장됩니다.
""")
            if select_work not in ['1', '2', '3', '4']:
                break
            else:
                while True:
                    fmt = input("""    
파일형식을 지정하세요
[ 1:png 2:jpeg 3:jpg 4:gif ] :
""")
                    if fmt not in ['1', '2', '3', '4']:
                        continue

                    L = []
                    format = {'1': 'png', '2': 'jpeg', '3': 'jpg', '4': 'gif'}
                    for i in work_list:
                        L.append(make_dir(i))

                    if select_work == '1':
                        for i in L:
                            r = trans_img_to_PIL(i[0])
                            trans_PIL_to_img(r, str(i[1]) + '\\' + i[0].stem + '.' + format[fmt])
                    elif select_work == '2':
                        prefix = input("prefix를 입력하세요 :")
                        for num, p_ in enumerate(L):
                            suffix = p_[0].suffix
                            target = str(p_[1]) + '\\' + prefix + str(num) + '.' + suffix
                            shutil.copy(p_[0], target)

                    elif select_work == '3':
                        print("기존 파일형식을 유지합니다.")
                        position = int(input('자를 위치 선택 [왼쪽:1 오른쪽: 2] :'))
                        w = int(input("자를 폭 선택 [W] :"))
                        for i in L:
                            r = trans_img_to_PIL(i[0])
                            if w >= r.size[0] or w >= r.size[1]:
                                print("%s보다 작은 폭을 선택하세요" % (max(r.size[0], r.size[1])))
                            else:
                                f = (i[0].suffix)
                                print(f)
                                if position == 1:
                                    c1 = r.crop((w, w, r.size[0], r.size[1]))
                                    trans_PIL_to_img(c1, str(i[1]) + '\\' + i[0].stem + f)
                                    print('done')
                                else:
                                    c1 = r.crop((0, 0, r.size[0] - w, r.size[1] - w))
                                    trans_PIL_to_img(c1, str(i[1]) + '\\' + i[0].stem + f)

                    elif select_work == '4':
                        width = int(input("이미지 size 입력 넓이[W] :"))
                        height = int(input("이미지 size 입력 높이[H] :"))
                        for i in L:
                            r = trans_img_to_PIL(i[0])
                            result = r.resize((width, height))
                            trans_PIL_to_img(result, str(i[1]) + '\\' + i[0].stem + '.' + format[fmt])

                    break

        exit()
        
        
        
        
'''

'''
file = "C:/Users/neo21/Downloads/introducing-python-master/introducing-python-master/2.png"
file2 = "C:/Users/neo21/Downloads/introducing-python-master/introducing-python-master/22.png"
memo = img_to_memory(file)
print(memo)
r = convert_image(memo)
result = memory_to_PIL(r)
print(result)
trans_PIL_to_img(result, file2)

'''
file = "C:/Users/neo21/Downloads/introducing-python-master/introducing-python-master/2.png"
file2 = "C:/Users/neo21/Downloads/introducing-python-master/introducing-python-master/22.png"
memo = img_to_memory(file)
print(memo)
result = memory_to_PIL(memo)
print(result)
trans_PIL_to_img(result, file2)

```