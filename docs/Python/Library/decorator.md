---
layout: default
title: decorator
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

데코레이터는 함수를 수정하지 않은 상태에서 추가 기능을 구현할 때 사용합니다.

## 데코레이터 만들기

- closure이용

```python
def trace(func):                             # 호출할 함수를 매개변수로 받음
    def wrapper():                           # 호출할 함수를 감싸는 함수
        print(func.__name__, '함수 시작')    # __name__으로 함수 이름 출력
        func()                               # 매개변수로 받은 함수를 호출
        print(func.__name__, '함수 끝')
    return wrapper                           # wrapper 함수 반환
 
def hello():
    print('hello')
 
def world():
    print('world')
 
trace_hello = trace(hello)    # 데코레이터에 호출할 함수를 넣음
trace_hello()                 # 반환된 함수를 호출
trace_world = trace(world)    # 데코레이터에 호출할 함수를 넣음
trace_world()                 # 반환된 함수를 호출
```
- @로 데코레이터 사용

```python
@데코레이터
def 함수이름():
    코드
```

```python
def trace(func):                             # 호출할 함수를 매개변수로 받음
    def wrapper():
        print(func.__name__, '함수 시작')    # __name__으로 함수 이름 출력
        func()                               # 매개변수로 받은 함수를 호출
        print(func.__name__, '함수 끝')
    return wrapper                           # wrapper 함수 반환
 
@trace    # @데코레이터
def hello():
    print('hello')
 
@trace    # @데코레이터
def world():
    print('world')
 
hello()    # 함수를 그대로 호출
world()    # 함수를 그대로 호출
```

- 2개 이상의 데커레이터 사용 : 실행 순서는 위에서 아래로

```python

def decorator1(func):
    def wrapper():
        print('decorator1')
        func()
    return wrapper
 
def decorator2(func):
    def wrapper():
        print('decorator2')
        func()
    return wrapper
 
# 데코레이터를 여러 개 지정
@decorator1
@decorator2
def hello():
    print('hello')
 
hello()

'''
decorator1
decorator2
hello
'''
```

hello = decorator1(decorator2(hello))
hello()

## 매개변수와 반환값을 처리하는 데코레이터 만들기

```python
def trace(func):  # 호출할 함수를 매개변수로 받음

    def wrapper(a, b):  # 호출할 함수 add(a, b)의 매개변수와 똑같이 지정
        r = func(a, b)  # func에 매개변수 a, b를 넣어서 호출하고 반환값을 변수에 저장
        print('{0}(a={1}, b={2}) -> {3}'.format(func.__name__, a, b,
                                                r))  # 매개변수와 반환값 출력
        return r  # func의 반환값을 반환

    return wrapper  # wrapper 함수 반환


@trace  # @데코레이터
def add(a, b):  # 매개변수는 두 개
    return a + b  # 매개변수 두 개를 더해서 반환


print(add(10, 20))

'''
add(a=10, b=20) -> 30
30
'''
```

### 가변 인수 함수 데코레이터

```python

def trace(func):  # 호출할 함수를 매개변수로 받음

    def wrapper(*args, **kwargs):  # 가변 인수 함수로 만듦
        r = func(*args, **kwargs)  # func에 args, kwargs를 언패킹하여 넣어줌
        print('{0}(args={1}, kwargs={2}) -> {3}'.format(
            func.__name__, args, kwargs, r))
        # 매개변수와 반환값 출력
        return r  # func의 반환값을 반환

    return wrapper  # wrapper 함수 반환


@trace  # @데코레이터
def get_max(*args):  # 위치 인수를 사용하는 가변 인수 함수
    return max(args)


@trace  # @데코레이터
def get_min(**kwargs):  # 키워드 인수를 사용하는 가변 인수 함수
    return min(kwargs.values())


print(get_max(10, 20))
print(get_min(x=10, y=20, z=30))

'''
get_max(args=(10, 20), kwargs={}) -> 20
20
get_min(args=(), kwargs={'x': 10, 'y': 20, 'z': 30}) -> 10
10
'''

```

###  메서드에 데코레이터 사용하기

클래스를 만들면서 메서드에 데코레이터를 사용할 때는 `self`를 주의해야 합니다.    
인스턴스 메서드는 항상 self를 받으므로 데코레이터를 만들 때도 wrapper 함수의 첫 번째 매개변수는 self로 지정해야 합니다(클래스 메서드는 `cls`).    
마찬가지로 데커레이터 함수 정의에서 func를 호출할 때도 `self와 매개변수를 그대로 넣어야 합니다`.

```python
decorator_method.py
def trace(func):
    def wrapper(self, a, b):   # 호출할 함수가 인스턴스 메서드이므로 첫 번째 매개변수는 self로 지정
        r = func(self, a, b)   # self와 매개변수를 그대로 넣어줌
        print('{0}(a={1}, b={2}) -> {3}'.format(func.__name__, a, b, r))   # 매개변수와 반환값 출력
        return r               # func의 반환값을 반환
    return wrapper
 
class Calc:
    @trace
    def add(self, a, b):    # add는 인스턴스 메서드
        return a + b
 
c = Calc()
print(c.add(10, 20))

'''
add(a=10, b=20) -> 30
30
'''
```
## 매개변수가 있는 데코레이터 만들기

```python
def is_multiple(x):  # 데코레이터가 사용할 매개변수를 지정

    def real_decorator(func):  # 호출할 함수를 매개변수로 받음

        def wrapper(a, b):  # 호출할 함수의 매개변수와 똑같이 지정
            r = func(a, b)  # func를 호출하고 반환값을 변수에 저장
            if r % x == 0:  # func의 반환값이 x의 배수인지 확인
                print('{0}의 반환값은 {1}의 배수입니다.'.format(func.__name__, x))
            else:
                print('{0}의 반환값은 {1}의 배수가 아닙니다.'.format(func.__name__, x))
            return r  # func의 반환값을 반환

        return wrapper  # wrapper 함수 반환

    return real_decorator  # real_decorator 함수 반환


@is_multiple(3)  # @데코레이터(인수)
def add(a, b):
    return a + b


print(add(10, 20))
print(add(2, 5))

'''
add의 반환값은 3의 배수입니다.
30
add의 반환값은 3의 배수가 아닙니다.
7
'''
```

### 매개변수가 있는 데코레이터를 여러 개 지정하기   

실행순서 : 아래서 위로

```python
@데코레이터1(인수)
@데코레이터2(인수)
def 함수이름():
    코드
```

```python
@is_multiple(3)
@is_multiple(7)
def add(a, b):
    return a + b

add(10, 20)
'''
add의 반환값은 7의 배수가 아닙니다.
wrapper의 반환값은 3의 배수입니다.
'''
```

decorated_add = is_multiple(3)(is_multiple(7)(add))
decorated_add(10, 20)

- 원래 함수 이름이 안나온다면?   

함수의 원래 이름을 출력하고 싶다면 functools 모듈의 wraps 데코레이터를 사용해야 합니다. 

@functools.wraps는 원래 함수의 정보를 유지시켜줍니다. 따라서 디버깅을 할 때 유용하므로 데코레이터를 만들 때는 @functools.wraps를 사용하는 것이 좋습니다.

```python 
import functools
 
def is_multiple(x):
    def real_decorator(func):
        @functools.wraps(func)    # @functools.wraps에 func를 넣은 뒤 wrapper 함수 위에 지정
        def wrapper(a, b):
            r = func(a, b)
            if r % x == 0:
                print('{0}의 반환값은 {1}의 배수입니다.'.format(func.__name__, x))
            else:
                print('{0}의 반환값은 {1}의 배수가 아닙니다.'.format(func.__name__, x))
            return r
        return wrapper
    return real_decorator
 
@is_multiple(3)
@is_multiple(7)
def add(a, b):
    return a + b
 
add(10, 20)
'''
add의 반환값은 7의 배수가 아닙니다.
add의 반환값은 3의 배수입니다.
'''
```
## 클래스로 데코레이터 만들기

클래스를 활용할 때는 인스턴스를 함수처럼 호출하게 해주는 `__call__` 메서드를 구현해야 합니다.

다음은 함수의 시작과 끝을 출력하는 데코레이터입니다.

```python
class Trace:
    def __init__(self, func):    # 호출할 함수를 인스턴스의 초깃값으로 받음
        self.func = func         # 호출할 함수를 속성 func에 저장
 
    def __call__(self):
        print(self.func.__name__, '함수 시작')    # __name__으로 함수 이름 출력
        self.func()                               # 속성 func에 저장된 함수를 호출
        print(self.func.__name__, '함수 끝')
 
@Trace    # @데코레이터
def hello():
    print('hello')
 
hello()    # 함수를 그대로 호출

'''
hello 함수 시작
hello
hello 함수 끝
'''
```
trace_hello = Trace(hello)    # 데코레이터에 호출할 함수를 넣어서 인스턴스 생성
trace_hello()                 # 인스턴스를 호출. __call__ 메서드가 호출됨

## 클래스로 매개변수와 반환값을 처리하는 데코레이터 만들기

```python
class Trace:
    def __init__(self, func):    # 호출할 함수를 인스턴스의 초깃값으로 받음
        self.func = func         # 호출할 함수를 속성 func에 저장
 
    def __call__(self, *args, **kwargs):    # 호출할 함수의 매개변수를 처리
        r = self.func(*args, **kwargs) # self.func에 매개변수를 넣어서 호출하고 반환값을 변수에 저장
        print('{0}(args={1}, kwargs={2}) -> {3}'.format(self.func.__name__, args, kwargs, r))
                                            # 매개변수와 반환값 출력
        return r                            # self.func의 반환값을 반환
 
@Trace    # @데코레이터
def add(a, b):
    return a + b
 
print(add(10, 20))
print(add(a=10, b=20))

'''
add(args=(10, 20), kwargs={}) -> 30
30
add(args=(), kwargs={'a': 10, 'b': 20}) -> 30
30
'''
```

## 클래스로 매개변수가 있는 데코레이터 만들기

마지막으로 매개변수가 있는 데코레이터를 만들어보겠습니다. 다음은 함수의 반환값이 특정 수의 배수인지 확인하는 데코레이터입니다.

```python
class IsMultiple:
    def __init__(self, x):         # 데코레이터가 사용할 매개변수를 초깃값으로 받음
        self.x = x                 # 매개변수를 속성 x에 저장
 
    def __call__(self, func):      # 호출할 함수를 매개변수로 받음
        def wrapper(a, b):         # 호출할 함수의 매개변수와 똑같이 지정(가변 인수로 작성해도 됨)
            r = func(a, b)         # func를 호출하고 반환값을 변수에 저장
            if r % self.x == 0:    # func의 반환값이 self.x의 배수인지 확인
                print('{0}의 반환값은 {1}의 배수입니다.'.format(func.__name__, self.x))
            else:
                print('{0}의 반환값은 {1}의 배수가 아닙니다.'.format(func.__name__, self.x))
            return r               # func의 반환값을 반환
        return wrapper             # wrapper 함수 반환
 
@IsMultiple(3)    # 데코레이터(인수)
def add(a, b):
    return a + b
 
print(add(10, 20))
print(add(2, 5))

'''
add의 반환값은 3의 배수입니다.
30
add의 반환값은 3의 배수가 아닙니다.
7
'''
```
### 연습문제

```python

def type_check(type_a, type_b):

    def real_decorator(func):

        def wrapper(a, b):
            if isinstance(a, type_a) and isinstance(b, type_b):
                return func(a, b)
            else:
                raise RuntimeError('자료형이 올바르지 않습니다.')

        return wrapper

    return real_decorator


@type_check(int, int)
def add(a, b):
    return a + b

try:
    print(add(10, 20))
    print(add('hello', 'world'))
except Exception as e:
    print(e)

'''
30
자료형이 올바르지 않습니다.
'''

```

```python
def html_tag(a):
    def wrapper1(func):
        r = func()
        def wrapper2():
            return '<{0}>{1}</{2}>'.format(a,r,a)
        return wrapper2
    return wrapper1

a, b = input().split()

@html_tag(a)
@html_tag(b)
def hello():
    return 'Hello, world!'

print(hello())
```
