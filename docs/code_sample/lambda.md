---
#title: Automated Deployment
title: lambda
parent: code_sample
---

# lambda

## 람다 표현식 호출

- 변수에 할당 후 호출
- 람다 표현식 자체를 호출하기 : (lambda 매개변수들: 식)(인수들)
- map,zip,filter등에서 람다 표현식을 인수로 사용하기

```python
plus_ten = lambda x: x + 10
result = plus_ten(1)

result = (lambda x: x + 10)(1)

result = list(map(lambda x: x + 10, [1, 2, 3]))
```
## 람다 표현식 특징
- 람다 표현식 안에서는 변수를 만들 수 없다
- 람다 표현식 바깥에 있는 변수는 사용할 수 있습니다. 
- 람다 표현식으로 매개변수가 없는 함수 만들기 가능
```python
(lambda x: y = 10; x + y)(1) # SyntaxError: invalid syntax

y = 10
result = (lambda x: x + y)(1)

result = (lambda : 1)()
```

## 람다 표현식에 조건부 표현식 사용하기
- lambda 매개변수들: 식1 if 조건식 else 식2
- lambda 매개변수들: 식1 if 조건식1 else 식2 if 조건식2 else 식3
```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
result = list(map(lambda x: str(x) if x % 3 == 0 else x, a)) # [1, 2, '3', 4, 5, '6', 7, 8, '9', 10]

a= [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
result = list(map(lambda x: str(x) if x == 1 else float(x) if x == 2 else x + 10, a))
print(result) # ['1', 2.0, 13, 14, 15, 16, 17, 18, 19, 20]
```
## map에 객체를 여러 개 넣기
map은 리스트 등의 반복 가능한 객체를 여러 개 넣을 수도 있습니다. 다음은 두 리스트의 요소를 곱해서 새 리스트를 만듭니다.
```python
a = [1, 2, 3, 4, 5]
b = [2, 4, 6, 8, 10]
result = list(map(lambda x, y: x * y, a, b)) # [2, 8, 18, 32, 50]
```

## filter 사용하기
```python
a = [8, 3, 2, 10, 15, 7, 1, 9, 0, 11]
result = list(filter(lambda x: x > 5 and x < 10, a)) # [8, 7, 9]
```
## reduce 사용하기 : 모든반복객체에 함수 적용
from functools import reduce
reduce(함수, 반복가능한객체)
```python
from functools import reduce

def f(x, y):
     return x + y

a = [1, 2, 3, 4, 5]
result = reduce(f, a) 
print(result) # 15
```

## map, filter, reduce와 리스트 표현식 비교(처리속도)
리스트(딕셔너리, 세트) 표현식으로 처리할 수 있는 경우에는 map, filter와 람다 표현식 대신 리스트 표현식을 사용하는 것이 좋습니다.
```python 
a = [8, 3, 2, 10, 15, 7, 1, 9, 0, 11]
result = list(filter(lambda x: x > 5 and x < 10, a))
result = [i for i in a if i > 5 and i < 10] 
# [8, 7, 9]
```