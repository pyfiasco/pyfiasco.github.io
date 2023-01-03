---
layout: default
title: pillow(PIL)
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

이미지 분석 및 처리를 쉽게 할 수 있는 라이브러리(Python Imaging Library : PIL)가 있습니다. 바로 pillow모듈입니다. 다양한 이미지 파일 형식을 지원하며, 강력한 이미지 처리와 그래픽 기능을 제공하는 이미지프로세싱 라이브러리의 한 종류입니다.
 
## 주요기능
PIL 이미지 작업을 위한 표준 절차를 제공하고 있으며, 다음과 같은 것이있다.(출처 :위키백과)
- 픽셀 단위의 조작
- 마스킹 및 투명도 제어
- 흐림, 윤곽 보정 다듬어 윤곽 검출 등의 이미지 필터
- 선명하게, 밝기 보정, 명암 보정, 색 보정 등의 화상 조정
- 이미지에 텍스트 추가
- 기타 여러가지

## Download and Documentation
- https://github.com/python-pillow
- https://pillow.readthedocs.io/en/stable/index.html

## 설치
pip install pillow

## 사용 예
![Alt text](/assets/images/%EC%95%84%EC%9D%B4%EC%9C%A0.png)
아이유 사진 출처 : twitter.com/IUsFairyTale

```python
from PIL import Image, ImageFilter  # 라이브러리를  임포트 한다.

original = Image.open("아이유.png")           # 하드 드라이브에서 이미지를 읽어 들인다.
blurred = original.filter(ImageFilter.BLUR) # 이미지를 흐리게 한다.
print(type(original)) # <class 'PIL.PngImagePlugin.PngImageFile'>
print(type(blurred))  # <class 'PIL.Image.Image'>

original.show() # 두 이미지를 디스플레이 한다.
blurred.show()
``` 

## Image 모듈 사용
```python
from PIL import Image
```

### 이미지 불러오기  및 이미지 보기
```python
img_obj = Image.open("아이유.png")  # 이미지 파일 불러오기
img_obj.show() # 이미지 보이기
```
- 이미지 파일관 호환 문제로 원본과 다른 파일 형식으로 저장 시 에러 발생   
    [해결책] 이미지 불러들일 때 형식을 변환하여 읽기
    img = Image.open("아이유.png").convert('RGB')

```python
convert('RGB') 함수 사용을 통해 이미지 모드를 통일하여 사용하자.

from PIL import Image

# 2. 이미지 파일 변환(정상) #
try:
    im = Image.open("anchors.png").convert('RGB')
    im.save("anchors.webp", 'webp')

    change_im = Image.open("anchors.webp")
    img_width, img_height = change_im.size
    print("이미지 확장자:", change_im.format)
    print("이미지 사이즈:", change_im.size)
    print("이미지 가로:", img_width)
    print("이미지 세로:", img_height)
    print("이미지 모드:", change_im.mode)
except OSError as e:
    print(e)


[output]
이미지 확장자: WEBP
이미지 사이즈: (600, 300)
이미지 가로: 600
이미지 세로: 300
이미지 모드: RGB

```


### 이미지 속성 확인
```python
print(f'파일 이름 : {img_obj.filename}')
print(f'파일형식(format) : {img_obj.format}')
print(f'용량(size) : {img_obj.size}')
print(f'색상모드 : {img_obj.mode}')
print(f'width : {img_obj.width}')
print(f'height : {img_obj.height}')
```
```
파일 이름 : 아이유.png
파일형식(format) : PNG
용량(size) : (425, 426)
색상모드 : RGBA
width : 425
height : 426
```
 
### 이미지 크기 변경하기 : resoze((w,h), option)
인자는 size 요소 - 튜플자료형
```python
# 이미지 size 1/2로 줄이기
w, h = img_obj.size
result_img = img_obj.resize((w // 2, h // 2))
result_img.show()
```
- option

<div class="code-example" markdown="1">

| 필터	             | 내용 |
|:-------------------|:----------------|
| PIL.Image.NEAREST  | 입력 이미지에서 가장 가까운 픽셀 하나를 선택합니다. 다른 모든 입력 픽셀은 무시합니다. |
| PIL.Image.BOX	     | 소스 이미지의 각 픽셀은 동일한 가중치를 가진 대상 이미지의 한 픽셀에 기여합니다. 업 스케일링의 경우 NEAREST. 이 필터는 resize() 및 thumbnail()메서드 에서만 사용할 수 있습니다 . |
| PIL.Image.BILINEAR | 크기 조정을 위해 출력 값에 기여할 수있는 모든 픽셀에서 선형 보간법을 사용하여 출력 픽셀 값을 계산합니다. 다른 변환의 경우 입력 이미지의 2x2 환경에 대한 선형 보간이 사용됩니다. |
| PIL.Image.HAMMING	 | BILINEAR보다 선명한 이미지를 생성합니다. BOX처럼 로컬 수준의 전위가 없습니다. 이 필터는 resize() 및 thumbnail()메서드 에서만 사용할 수 있습니다 . |
| PIL.Image.BICUBI	| 크기 조정을 위해 출력 값에 기여할 수 있는 모든 픽셀에서 삼차 보간법을 사용하여 출력 픽셀 값을 계산합니다. 다른 변환의 경우 입력 이미지의 4x4 환경에 대한 큐빅 보간이 사용됩니다. |
| PIL.Image.LANCZOS	| 출력 값에 기여할 수있는 모든 픽셀에서 고품질 Lanczos 필터 (잘린 sinc)를 사용하여 출력 픽셀 값을 계산합니다. 이 필터는 resize() 및 thumbnail()메서드 에서만 사용할 수 있습니다 . |

</div>
 
### 이미지 자르기 : crop((left, upper, right, lower))
![Alt text](/assets/images/picture6.png)


```python
cropped_img = img.crop((200, 200, 425, 426))
cropped_img.show()
``` 
### 이미지 회전 : rotate(회전각도)
```python 
result_img = img_obj.rotate(45) # 45도 회전(반시계방향)
result_img.show()
```

### 이미지 상하, 좌우 대칭 : transpose(옵션) 

옵션
- Image.FLIP_LEFT_RIGHT : 좌우 대칭처리
- Image.FLIP_TOP_BOTTOM : 상하 대칭처리
- 회전처리
  Image.ROTATE_90 : 90도 회전
  Image.ROTATE_180: 180도 회전
  Image.ROTATE_270: 270도 회전

```python
result_img = img_obj.transpose(Image.FLIP_LEFT_RIGHT)
result_img.show()
```

```python
result_img = img_obj.transpose(Image.ROTATE_270)
result_img.show()
```

### 이미지 합치기 : new(mode,size,color)

<div class="code-example" markdown="1">

|:---------------------------------------|:-----------|:--------------------------------------------------------|:---------------------------------------|
| ![Alt text](/assets/images/아이유.png) | ![Alt text](/assets/images/1.png) | ![Alt text](/assets/images/2.png) | ![Alt text](/assets/images/save.png) |

</div><br>            

```python
from PIL import Image, ImageFilter

# 이미지 불러오기
img1 = Image.open('아이유.png')
img2 = Image.open('1.png')
img3 = Image.open('2.png')

# 새 이미지 만들기
new_img = Image.new('RGBA',(700,700),(255, 192, 0))

# 이미지 붙이기
new_img.paste(img1, (10,10))     # left,top 위치만 지정
new_img.paste(img2,(20+img1.width,10))
new_img.paste(img3,(20+img1.width,20+img2.height))

new_img.show()
```
 
### 이미지 저장

```python
from PIL import Image, ImageFilter

# 이미지 불러오기
img_obj = Image.open('아이유.png')
img_obj.save('아이유2.png')

result_obj = Image.open('아이유2.png')
result_obj.show()
```

### thumbnail 만들기

```python
from PIL import Image
size = (40, 40)  #튜플자료형으로 괄호 생략 가능(#<class 'tuple'>)

img_obj = Image.open("아이유.png")
img_obj.thumbnail(size)

img_obj.save("아이유3.png")
result_img = Image.open("아이유3.png")
result_img.show()
```


## ImageFilter 모듈 사용 

```python
from PIL import Image, ImageFilter
img_obj = Image.open("아이유.png")  # 하드 드라이브에서 이미지를 읽어 들인다.
```

Image.filter()함수를 사용하여 이미지 필터 적용
- BLUR
- CONTOUR
- DETAIL
- EDGE_ENHANCE
- EDGE_ENHANCE_MORE
- EMBOSS
- FIND_EDGES
- SHARPEN
- SMOOTH
- SMOOTH_MORE

### Blur 처리

옵션
ImageFilter.BLUR : 고정된 값으로 Blur처리
ImageFiler.BoxBlur()함수
ImageFilter.GaussianBlur()함수

```python
result_img = img_obj.filter(ImageFilter.BLUR)
result_img.show()

result_img = img_obj.filter(ImageFilter.BoxBlur(10))
result_img.show()

result_img = img_obj.filter(ImageFilter.GaussianBlur(10))
result_img.show()
```
```python
#전체옵션 보기
from PIL import Image, ImageFilter

img_obj = Image.open("아이유.png")  # 하드 드라이브에서 이미지를 읽어 들인다.

filter_list = [ImageFilter.BLUR, ImageFilter.CONTOUR, ImageFilter.DETAIL,
               ImageFilter.EDGE_ENHANCE, ImageFilter.EDGE_ENHANCE_MORE,
               ImageFilter.EMBOSS, ImageFilter.FIND_EDGES,
               ImageFilter.SHARPEN, ImageFilter.SMOOTH,
               ImageFilter.SMOOTH_MORE]

for i in range(len(filter_list)):
    result_img = img_obj.filter(filter_list[i])
    # filter_img.save("C:/Users/ilike/Pictures/filter_img_{}.jpg".format(i))
    result_img.show()
```
 
## 이미지 처리

### 현재 디렉토리의 모든 png 이미지를 썸네일로 만들기

```python

from PIL import Image
import glob, os, pathlib

target = glob.glob("./*.png")
print("파일 개수 :", len(target))
size = (40, 40)  #튜플자료형으로 괄호 생략 가능(#<class 'tuple'>)
for file in target:
    file_path = pathlib.Path('.') / file
    img_obj = Image.open(file)
    img_obj.thumbnail(size)

    img_obj.save(file_path.stem + ".thumbnail"+".png")

```

### 이미지를 바이트배열(bytearray)로 변환

io.BytesIO()를 사용하여 이미지를 byte array로 변환

```python
from PIL import Image
import io

def image_to_byte_array(image):
    img_obj = Image.open(image)
    byte_arr = io.BytesIO()
    img_obj.save(byte_arr, format=img_obj.format)
    return byte_arr.getvalue()
img = "아이유.png"
print(image_to_byte_array(img))
```

### 이미지를 넘파이 배열로 변환

numpy.array()함수를 사용하여 이미지를 배열 객체로 반환할 수 있습니다.

```python
from PIL import Image
import numpy as np
img = Image.open("아이유.png")

numpy_img = np.array(img)
print(type(numpy_img))
print(numpy_img)
```
```
#실행결과
<class 'numpy.ndarray'>
[[[246 246 248]
  [246 246 248]
  [246 246 248]
  ...
  [242 241 246]
  [242 241 246]
  [242 241 246]]
  .....이하생략
```

### 넘파이(numpy) 배열을 이미지로 변환

```python
from PIL import Image
import numpy as np
img = Image.open("아이유.png")

#numpy_array = np.array(img, dtype="uint8")
numpy_array = np.array(img)
   
image2 = Image.fromarray(numpy_array, 'RGB')
image2.show() 
```

### 이미지를 픽셀 값으로 변환

```python
from PIL import Image
import numpy as np
img = Image.open("아이유.png")

pixel_list = list(img.getdata())
print(pixel_list)
np.savetxt("pixel_type_data.txt", pixel_list, fmt='%d', delimiter=" ")
```

### 이미지의 특정 픽셀의 RGB 색상 구하기


convert()함수를 사용하여 RGB 데이터를 가져옵니다.    
그런 다음, getpixel()함수를 사용하여 특정 픽셀의  x, y  좌표값을 지정하면 픽셀값을 튜플자료형으로 반환합니다.

```python
from PIL import Image
img = Image.open("C:/Users/ilike/Pictures/IU_400x400.jpg")

rgb_img = img.convert("RGB")

#지정한 좌표값의 픽셀값 튜플자료형으로 반환
tuple_item = rgb_img.getpixel((1, 100))
print(tuple_item) 

r, g, b = tuple_item
print(r)
print(g)
print(b)
```
```
#실행결과
(244, 245, 249)
244
245
249
``` 

## 이미지 관리 프로그램
```python
from io import BytesIO
from PIL import Image
import sys


def data_to_img(data):
    """Return PIL Image object, with data from in-memory <data>"""
    # open함수와 비슷한 기능
    fp = BytesIO(data)
    return Image.open(fp)  # reads from memory


def img_to_data(img, fmt=None):
    """Return image data from PIL Image <img>, in <fmt> format"""
    fp = BytesIO()
    if not fmt:
        fmt = img.format  # keeps the original format
        img.save(fp, fmt)  # writes to memory
    return fp.getvalue()


def convert_image(data, fmt=None):
    """Convert image <data> to PIL <fmt> image data"""
    img = data_to_img(data)
    return img_to_data(img, fmt)


def get_file_data(name):
    """Return PIL Image object for image file <name>"""
    img = Image.open(name)
    print("img", img, img.format)
    return img_to_data(img)


if __name__ == "__main__":
    for name in sys.argv[1:]:
        data = get_file_data(name)
        print("in", len(data), data[:10])
    for fmt in ("gif", "png", "jpeg"):
        outdata = convert_image(data, fmt)
        print("out", len(outdata), outdata[:10])
```