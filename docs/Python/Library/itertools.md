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


## iterable & iterator   

이터레이터를 만들기 전에 먼저 `반복 가능한 객체(iterable)`에 대해 알아보겠습니다.      
반복 가능한 객체는 말 그대로 반복할 수 있는 객체인데 우리가 흔히 사용하는 문자열, 리스트, 딕셔너리, 세트, range객체가 반복 가능한 객체입니다. 즉, 요소가 여러 개 들어있고, 한 번에 하나씩 꺼낼 수 있는 객체입니다.   
객체가 반복 가능한 객체인지 알아보는 방법은 객체에 `__iter__` 메서드가 들어있는지 확인해보면 됩니다. dir(객체)   

`반복 가능한 객체(iterable)`는 요소를 한 번에 하나씩 가져올 수 있는 객체이고, `이터레이터(iterator)`는 `__next__` 메서드를 사용해서 차례대로 값을 꺼낼 수 있는 객체입니다. `반복 가능한 객체(iterable)`와 `이터레이터(iterator)`는 별개의 객체이므로 둘은 구분해야 합니다.    

이처럼 `반복 가능한 객체`는 `__iter__` 메서드로 `이터레이터`를 얻고, `이터레이터`의 `__next__` 메서드로 반복합니다.


```python
L = ['a', 'b', 'c']
it = L.__iter__()  # iter(L)
print(it.__next__())  # a
print(it.__next__())  # b
print(it.__next__())  # c
# print(it.__next__())  # StopIteration 예외를 발생
```
리스트, 튜플, range, 문자열은 반복 가능한 객체이면서 시퀀스 객체입니다.    
하지만, 딕셔너리와 세트는 반복 가능한 객체이지만 시퀀스 객체는 아닙니다. 

![Alt text](/assets/images/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202023-01-14%20101856.png)

## 이터레이터 만들기

이제 `__iter__`, `__next__` 메서드를 구현해서 직접 이터레이터를 만들어보겠습니다.   

```python
class 이터레이터이름:

    def __iter__(self):
        코드

    def __next__(self):
        코드
```

간단하게 range(횟수)처럼 동작하는 이터레이터입니다.

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

다음 코드 추가   

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

### 심화 학습 예제

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


g = number_generator()
for i in g:
    print(i, end=' ')  # 0 1 2

print()
print(dir(g))  # __iter__, __next__ 존재
```

- next 구현

```python
g = number_generator()
while True:
    try:
        print(g.__next__(), end=' ')
    except:
        pass
```

![Alt text](/assets/images/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202023-01-15%20050230.png)

- yield & return      
이렇게 제너레이터는 함수를 끝내지 않은 상태에서 yield를 사용하여 값을 바깥으로 전달할 수 있습니다. 즉, `return`은 반환 즉시 함수가 끝나지만 `yield`는 잠시 함수 바깥의 코드가 실행되도록 양보하여 값을 가져가게 한 뒤 다시 제너레이터 안의 코드를 계속 실행하는 방식입니다. 

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
    - yield from 반복가능한객체
    - yield from 이터레이터
    - yield from 제너레이터객체

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

## coroutine

코루틴(coroutine)은 `cooperative routine`를 의미하는데 서로 협력하는 루틴이라는 뜻입니다.    
즉, 메인 루틴과 서브 루틴처럼 종속된 관계가 아니라 서로 `대등한 관계`이며 특정 시점에 상대방의 코드를 실행합니다.

참고로 함수의 코드를 실행하는 지점을 진입점(entry point)이라고 하는데, 코루틴은 `진입점`이 여러 개인 함수입니다.


### 코루틴에 값 보내기

코루틴은 제너레이터의 특별한 형태입니다.    
제너레이터는 yield로 값을 발생시켰지만 코루틴은 `(yield)`로 값을 받아올 수 있습니다.  => 변수 = (yield)   
메인 프로시저에서 코루틴에 값을 보내면서 코드를 실행할 때는 `send 메서드`를 사용합니다 => 코루틴객체.send(값)   

[참조] next와 send의 차이를 살펴보면 next는 코루틴의 코드를 실행하지만 값을 보내지 않을 때 사용하고,    
        send는 값을 보내면서 코루틴의 코드를 실행할 때 사용합니다.   

```python
def number_coroutine():
    while True:        # 코루틴을 계속 유지하기 위해 무한 루프 사용
        x = (yield)    # 코루틴 바깥에서 값을 받아옴, yield를 괄호로 묶어야 함
        print(x)
 
co = number_coroutine()
next(co)      # 코루틴 안의 yield까지 코드 실행(최초 실행) = co.send(None)
 
co.send(1)    # 코루틴에 숫자 1을 보냄
co.send(2)    # 코루틴에 숫자 2을 보냄
co.send(3)    # 코루틴에 숫자 3을 보냄
```

corotuine 진행
최초 진입 - 첫 yield 까지
이후 진행 - 데이터 받고 다음 yield까지
![Alt text](/assets/images/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202023-01-15%20082158.png)

{: .note}
> 코루틴객체.send(None)과 같이 send 메서드에 None을 지정해도 코루틴의 코드를 최초로 실행할 수 있습니다.

### 코루틴 바깥으로 값 전달하기

`(yield 변수)` 형식으로 yield에 변수를 지정한 뒤 괄호로 묶어주면 값을 받아오면서 바깥으로 값을 전달합니다.    
그리고 yield를 사용하여 바깥으로 전달한 값은 `next 함수(__next__ 메서드)`와 `send 메서드`의 반환값으로 나옵니다.

[coroutine]

- 변수 = (yield 변수)

[main process]

- 변수 = next(코루틴객체)
- 변수 = 코루틴객체.send(값)

```python
def sum_coroutine():
    total = 0
    while True:
        x = (yield total)    # 코루틴 바깥에서 값을 받아오면서 바깥으로 값을 전달
        total += x
 
co = sum_coroutine()
print(next(co))      # 0: 코루틴 안의 yield까지 코드를 실행하고 코루틴에서 나온 값 출력
 
print(co.send(1))    # 1: 코루틴에 숫자 1을 보내고 코루틴에서 나온 값 출력
print(co.send(2))    # 3: 코루틴에 숫자 2를 보내고 코루틴에서 나온 값 출력
print(co.send(3))    # 6: 코루틴에 숫자 3을 보내고 코루틴에서 나온 값 출력
```

![Alt text](/assets/images/%ED%99%94%EB%A9%B4%20%EC%BA%A1%EC%B2%98%202023-01-15%20083731.png)

```python
def find(word):
    result = False
    while True:        
        x = (yield result)
        result = word in x


f = find('Python')
next(f)

print(f.send('Hello, Python!'))
print(f.send('Hello, world!'))
print(f.send('Python Script'))

f.close()
```

- `제너레이터`와 `코루틴`의 차이점   
제너레이터는 `next 함수(__next__ 메서드)`를 반복 호출하여 값을 얻어내는 방식   
코루틴은 `next 함수(__next__ 메서드)`를 한 번만 호출한 뒤 `send`로 값을 주고 받는 방식   

- 값을 보내지 않고 코루틴의 코드 실행하기   
값을 보내지 않으면서 코루틴의 코드를 실행할 때는 `next 함수(__next__ 메서드)`만 사용하면 됩니다.    
잘 생각해보면 이 방식이 일반적인 제너레이터입니다.   

### 코루틴을 종료하고 예외 처리하기

만약 코루틴을 강제로 종료하고 싶다면 `close 메서드`를 사용합니다. : 코루틴객체.close()    

```python
def number_coroutine():
    while True:
        x = (yield)
        print(x, end=' ')
 
co = number_coroutine()
next(co)
 
for i in range(20):
    co.send(i)
 
co.close()    # 코루틴 종료
```

**GeneratorExit** 예외 처리하기

close 메서드를 호출하면 코루틴이 종료될 때 GeneratorExit 예외가 발생합니다. 따라서 이 예외를 처리하면 코루틴의 종료 시점을 알 수 있습니다.

```python
def number_coroutine():
    try:
        while True:
            x = (yield)
            print(x, end=' ')
    except GeneratorExit:  # 코루틴이 종료 될 때 GeneratorExit 예외 발생
        print()
        print('코루틴 종료')


co = number_coroutine()
next(co)

for i in range(20):
    co.send(i)

co.close()
```

코루틴 안에서 예외 발생시키기

throw메서드로 예외를 던진다.지정된 메시지는 except as의 변수에 들어갑니다 : 코루틴객체.throw(예외이름, 에러메시지)
except문에서 yield 값이 생성되면 반환값으로 반환된다.   

```python
def sum_coroutine():
    try:
        total = 0
        while True:
            x = (yield)
            total += x
    except RuntimeError as e:
        print(e)
        yield total    # 코루틴 바깥으로 값 전달
 
co = sum_coroutine()
next(co)
 
for i in range(20):
    co.send(i)
 
print(co.throw(RuntimeError, '예외로 코루틴 끝내기')) # 190 반환 - except문에서 생성된 yield 값

'''
예외로 코루틴 끝내기
190
'''
```

제너레이터에서 yield from을 사용하면 값을 바깥으로 여러 번 전달한다고 했습니다.    
하지만 `yield from 코루틴()`를 지정하면 해당 코루틴에서 return으로 반환한 값을 가져옵니다.   

변수 = yield from 코루틴()
다음은 코루틴에서 숫자를 누적한 뒤 합계를 yield from으로 가져옵니다.

```python
def accumulate():
    total = 0
    while True:
        x = (yield)  # 코루틴 바깥에서 값을 받아옴
        if x is None:  # 받아온 값이 None이면
            return total  # 합계 total을 반환
        total += x


def sum_coroutine():
    while True:
        total = yield from accumulate()  # accumulate의 반환값을 가져옴
        print(total)


co = sum_coroutine()
next(co)

for i in range(1, 11):  # 1부터 10까지 반복
    co.send(i)  # 코루틴 accumulate에 숫자를 보냄
co.send(None)  # 코루틴 accumulate에 None을 보내서 숫자 누적을 끝냄

for i in range(1, 101):  # 1부터 100까지 반복
    co.send(i)  # 코루틴 accumulate에 숫자를 보냄
co.send(None)  # 코루틴 accumulate에 None을 보내서 숫자 누적을 끝냄
```

- 코루틴 내에서 StopIteration 예외 발생시키기

raise로 StopIteration 예외를 직접 발생시키면 RuntimeError로 바뀌므로 이 방법은 사용할 수 없습니다.   
파이썬 3.7부터는 그냥 return 값을 사용해주세요.


- 코루틴의 yield from으로 값을 발생시키기
이번 예제에서는 x = (yield)와 같이 코루틴 바깥에서 보낸 값만 받아왔습니다. 하지만 코루틴에서 yield에 값을 지정해서 바깥으로 전달했다면 yield from은 해당 값을 다시 바깥으로 전달합니다.

```python
def number_coroutine():
    x = None
    while True:
        x = (yield x)    # 코루틴 바깥에서 값을 받아오면서 바깥으로 값을 전달
        if x == 3:
            return x
 
def print_coroutine():
    while True:
        x = yield from number_coroutine()   # 하위 코루틴의 yield에 지정된 값을 다시 바깥으로 전달
        print('print_coroutine:', x)
 
co = print_coroutine()
next(co)
 
x = co.send(1)    # number_coroutine으로 1을 보냄
print(x)          # 1: number_coroutine의 yield에서 바깥으로 전달한 값
x = co.send(2)    # number_coroutine으로 2를 보냄
print(x)          # 2: number_coroutine의 yield에서 바깥으로 전달한 값
co.send(3)        # 3을 보내서 반환값을 출력하도록 만듦

'''
1
2
print_coroutine: 3
'''

```




def calc():
    result =0
    while True:
        ex = (yield result)
        target = ex.split()
        x = int(target[0])
        y = int(target[2])
        if target[1] =='+':
            result = x + y
        if target[1] =='-':
            result = x - y
        if target[1] =='*':
            result = x * y        
        if target[1] =='/':
            result = x / y   
                 
expressions = '3 * 4, 10 / 5, 20 + 39'.split(', ')

c = calc()
next(c)

for e in expressions:
    print(c.send(e))

c.close()