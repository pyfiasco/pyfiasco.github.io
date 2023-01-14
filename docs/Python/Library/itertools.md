---
layout: default
title: itertools
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


## Iterate over Code Structures with itertools

```python
import itertools
it1 = itertools.chain([1, 2], ['a', 'b'])
print(it1)
for item in it1:
    print (item) # 1/2/a/b
'''
for item in itertools.cycle([1, 2]): # 무한 생성
    print (item)        
'''

it1 = itertools.accumulate([1, 2, 3, 4])
print(it1)
for item in it1:
    print (item) # 1/3/6/10


def multiply(a, b):
    return a * b

for item in itertools.accumulate([1, 2, 3, 4], multiply):
    print (item)  # 1/2/6/24
```



이터레이터를 만들기 전에 먼저 `반복 가능한 객체(iterable)`에 대해 알아보겠습니다.    
반복 가능한 객체는 말 그대로 반복할 수 있는 객체인데 우리가 흔히 사용하는 문자열, 리스트, 딕셔너리, 세트, range객체가 반복 가능한 객체입니다. 즉, 요소가 여러 개 들어있고, 한 번에 하나씩 꺼낼 수 있는 객체입니다.
객체가 반복 가능한 객체인지 알아보는 방법은 객체에 `__iter__` 메서드가 들어있는지 확인해보면 됩니다. dir(객체)

`반복 가능한 객체(iterable)`는 요소를 한 번에 하나씩 가져올 수 있는 객체이고, `이터레이터(iterator)`는 `__next__` 메서드를 사용해서 차례대로 값을 꺼낼 수 있는 객체입니다. `반복 가능한 객체(iterable)`와 `이터레이터(iterator)`는 별개의 객체이므로 둘은 구분해야 합니다. 

이처럼 `반복 가능한 객체`는 `__iter__` 메서드로 `이터레이터`를 얻고, `이터레이터`의 `__next__` 메서드로 반복합니다.


```python
L = ['a','b','c']
it = L.__iter__()
print(it.__next__()) # a
print(it.__next__()) # b
print(it.__next__()) # c
print(it.__next__()) # StopIteration 예외를 발생
```
리스트, 튜플, range, 문자열은 반복 가능한 객체이면서 시퀀스 객체입니다.    
하지만, 딕셔너리와 세트는 반복 가능한 객체이지만 시퀀스 객체는 아닙니다. 

![Alt text](/assets/images/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202023-01-14%20101856.png)

## 이터레이터 만들기

이제 `__iter__`, `__next__` 메서드를 구현해서 직접 이터레이터를 만들어보겠습니다.    
간단하게 range(횟수)처럼 동작하는 이터레이터입니다.

```python
class 이터레이터이름:

    def __iter__(self):
        코드

    def __next__(self):
        코드
```

```python
class Counter:

    def __init__(self, stop):
        self.current = 0  # 현재 숫자 유지, 0부터 지정된 숫자 직전까지 반복
        self.stop = stop  # 반복을 끝낼 숫자

    def __iter__(self):
        return self  # 현재 인스턴스를 반환

    def __next__(self):
        if self.current < self.stop:  # 현재 숫자가 반복을 끝낼 숫자보다 작을 때
            r = self.current  # 반환할 숫자를 변수에 저장
            self.current += 1  # 현재 숫자를 1 증가시킴
            return r  # 숫자를 반환
        else:  # 현재 숫자가 반복을 끝낼 숫자보다 크거나 같을 때
            raise StopIteration  # 예외 발생

for i in Counter(3):
    print(i, end=' ')    # 0 1 2
```

- map객체도 iterator다.

```python
a, _, c = map(str,Counter(3))
print(a,c)
```

## 인덱스로 접근할 수 있는 이터레이터 만들기
`__getitem__` 메서드를 구현하여 `인덱스로 접근할 수 있는 이터레이터`를 만들어보겠습니다.


```python
class 이터레이터이름:
    def __getitem__(self, 인덱스):
        코드
```

```python
    def __getitem__(self, index):
        if index < self.stop:
            return index
        else:
            raise IndexError
        

for i in Counter(3):
    print(Counter(3)[i], end=' ') # 0 1 2
```

{: .note}
> `__init__` 메서드와 `__getitem__` 메서드만 있어도 iterator 생성 가능(초기화 불필요시 `__getitem__`메서드만으로도 구현 가능)    
즉 `__getitem__`만 구현해도 이터레이터가 되며 `__iter__`, `__next__`는 생략해도 됩니다.

## list에 __next__메서를 추가하여 iterator 구현

```python
class Counter(list):

    def __init__(self, *args):
        super().__init__(args)
        self.current = 0  

    def __next__(self):
        if self.current < len(self):  
            r = self.current  
            self.current += 1  
            return self[r]  
        else:  
            raise StopIteration  

a = Counter(11,8,4,76,123,4)
for i in a:
    print(a.__next__())
```

## iter, next 함수 활용하기

반복 가능한 객체에서 `__iter__`를 호출하고 이터레이터에서 `__next__` 메서드를 호출한 것과 똑같습니다.    
즉, `iter`는 반복 가능한 객체에서 이터레이터를 반환하고, `next`는 이터레이터에서 값을 차례대로 꺼냅니다.    
`iter`와 `next`는 이런 기능 이외에도 다양한 방식으로 사용할 수 있습니다.

### iter
iter는 반복을 끝낼 값을 지정하면 특정 값이 나올 때 반복을 끝냅니다.    
이 경우에는 반복 가능한 객체 대신 `호출 가능한 객체(callable)`를 넣어줍니다.    
참고로 반복을 끝낼 값은 `sentinel`이라고 부르는데 감시병이라는 뜻입니다. 즉, 반복을 감시하다가 특정 값이 나오면 반복을 끝낸다고 해서 sentinel입니다.

- iter(호출가능한객체, 반복을끝낼값)

```python
import random
it = iter(lambda : random.randint(0, 10), 2)
while True:
   try:
       print(next(it), end=' ')
   except:
       break
```

### next

next는 기본값을 지정할 수 있습니다. 기본값을 지정하면 반복이 끝나더라도 StopIteration이 발생하지 않고 기본값을 출력합니다.    

- next(반복가능한객체, 기본값)

```python
import random
it = iter(lambda : random.randint(0, 10), 2)
while True:
   try:
       print(next(it, 10), end=' ')   # 무한 loop발생
   except:       
       break
```

심화 학습

```python
class TimeIterator:
    
    def calc(self,sec):
        a,b = divmod(sec,60)
        c,d = divmod(a,60)
        e,f = divmod(c,24)
        s = ":".join([str(f).zfill(2) , str(d).zfill(2) , str(b).zfill(2)])
        return s

    def __init__(self,start,stop):
        self.start = start
        self.stop = stop
        self.current = 0
        
    def __next__(self):
        if self.current < (self.stop - self.start):
            r = self.current
            result = r+self.start
            self.current +=1
            return self.calc(result)
        else:
            raise StopIteration
        
    def __iter__(self):
        return self
    
    def __getitem__(self,index):
        for i in range(index+1):
            result =  self.__next__()
        return result  


start, stop, index = [88234, 88255, 10] # map(int, input().split())

for i in TimeIterator(start, stop):
    print(i)

print('\n', TimeIterator(start, stop)[index], sep='')
```

## generator

### 제너레이터 사용하기
제너레이터는 이터레이터를 생성해주는 함수입니다. 이터레이터는 클래스에 `__iter__`, `__next__` 또는 `__getitem__` 메서드를 구현해야 하지만 제너레이터는 `함수 안에서 yield라는 키워드만 사용하면 끝`입니다. (StopIteration 자동 생성)  

함수 안에서 yield를 사용하면 함수는 제너레이터가 되며 yield에는 값(변수)을 지정합니다.

- yield 값

```python
def number_generator():
    yield 0
    yield 1
    yield 2

g =  number_generator() 
for i in g:
    print(i, end = ' ') # 0 1 2

 
print(dir(g))   # __iter__, __next__ 존재
```

next 구현

```python
g = number_generator()
while True:
    try:
        print(g.__next__(), end=' ')
    except:
        pass
```

![Alt text](/assets/images/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202023-01-15%20050230.png)
이렇게 제너레이터는 함수를 끝내지 않은 상태에서 yield를 사용하여 값을 바깥으로 전달할 수 있습니다. 즉, return은 반환 즉시 함수가 끝나지만 yield는 잠시 함수 바깥의 코드가 실행되도록 양보하여 값을 가져가게 한 뒤 다시 제너레이터 안의 코드를 계속 실행하는 방식입니다. 

{: .note}
> 제너레이터와 return
제너레이터는 함수 끝까지 도달하면 StopIteration 예외가 발생합니다. 마찬가지로 return도 함수를 끝내므로 return을 사용해서 함수 중간에 빠져나오면 StopIteration 예외가 발생합니다.
>
> 특히 제너레이터 안에서 return에 반환값을 지정하면 StopIteration 예외의 에러 메시지로 들어갑니다.

```python
def one_generator():
    yield 1
    return 'return에 지정한 값'
 
try:
    g = one_generator()
    next(g)
    next(g)
except StopIteration as e:
    print(e)    # return에 지정한 값
```

### generator 만들기

```python
def number_generator(stop):
    n = 0              # 숫자는 0부터 시작
    while n < stop:    # 현재 숫자가 반복을 끝낼 숫자보다 작을 때 반복
        yield n        # 현재 숫자를 바깥으로 전달
        n += 1         # 현재 숫자를 증가시킴
 
for i in number_generator(3):
    print(i)

```

```python
def upper_generator(x):
    for i in x:
        yield i.upper()    # 함수의 반환값을 바깥으로 전달
 
fruits = ['apple', 'pear', 'grape', 'pineapple', 'orange']
for i in upper_generator(fruits):
    print(i)
```

### yield from으로 값을 여러 번 바깥으로 전달하기

- for문을 이용한 생성 전달

```python
def number_generator():
    x = [1, 2, 3]
    for i in x:
        yield i
 
for i in number_generator():
    print(i)
```

- yield from 이용하여 생성 전달       
    : yield from 반복가능한객체(이터레이터,제너레이터객체)

```python
def number_generator():
    x = [1, 2, 3]
    yield from x    # 리스트에 들어있는 요소를 한 개씩 바깥으로 전달
                    # yield from문 1번 실행으로 3개의 iterable 데이터 생성
 
for i in number_generator():
    print(i)
```
```python
def number_generator(stop):
    n = 0
    while n < stop:
        yield n
        n += 1
 
def three_generator():
    yield from number_generator(3)    # 숫자를 세 번 바깥으로 전달
 
for i in three_generator():
    print(i)
```

```python
def file_read():
    with open('words.txt','r') as f:
        while True:
            line = f.readline()
            if line == '':
                break
            yield  line.strip('\n')        

for i in file_read():
    print(i)
```

소수 제너레이터

```python
def prime_number(start,stop):
    L = []
    for i in range(start,stop):
        for j in (range(2,i+1)):
            if i %j == 0 and i != j:
                break
            elif i %j == 0 and i == j:
                L.append(i)            
    return L

def prime_number_generator(start,stop):
    
    yield from prime_number(start,stop)
    return 'StopIterator'    
            

start, stop = map(int, input().split())

g = prime_number_generator(start, stop)
print(type(g))
for i in g:
    print(i, end=' ')
```


{: .note}
> 제너레이터 표현식
리스트 표현식을 사용할 때 [ ](대괄호)를 사용했습니다. 같은 리스트 표현식을 ( )(괄호)로 묶으면 제너레이터 표현식이 됩니다. 리스트 표현식은 처음부터 리스트의 요소를 만들어내지만 제너레이터 표현식은 필요할 때 요소를 만들어내므로 메모리를 절약할 수 있습니다.
>
> - (식 for 변수 in 반복가능한객체)

```python
>>> [i for i in range(50) if i % 2 == 0]
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48]
>>> (i for i in range(50) if i % 2 == 0)
<generator object <genexpr> at 0x024F02A0>
```






