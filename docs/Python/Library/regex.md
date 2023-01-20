---
layout: default
title: regular expression
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

## re 기능

```python
import re
result = re.match('Hello', 'Hello, world!')     # 정규표현식이 대상 문자열 처음에  매치 => match 객체가 반환됨
print(result) # <_sre.SRE_Match object; span=(0, 5), match='Hello'>
result = re.search('world', 'Hello, world!')  # 정규표현식이 대상 문자열에  매치 => match 객체가 반환됨
print(result) # <re.Match object; span=(7, 12), match='world'>
result = re.findall('l', 'Hello, world!')    # 매치하는 모든 문자열 list화
print(result) # ['l', 'l', 'l']
# re.sub('패턴', '바꿀문자열', '문자열', 바꿀횟수)
result = re.sub('l',"t", 'Hello, world!',2)    # replace 구현
print(result) # Hetto, world!
sp = re.split("a","speaking")
print(sp) # ['spe', 'king']
```

{: .note}
> 패턴_객체 = re.compile('패턴')             # 패턴객체 생성
매치_객체 = 패턴_객체.match('문자열')       # match객체 생성
매치_객체 = 패턴_객체.search('문자열')      # match객체 생성

```python
p = re.compile('[0-9]+')
m1 = p.match('1234')  # <re.Match object; span=(0, 4), match='1234'>
print(m1)

m2 = p.search('hello')
print(m2) # None
```           

## 표현식

1. 지정된 문자열이 하나라도 포함되는지 판단하기 
    문자열`|`문자열`|`문자열`|`문자열   

```python
result = re.match('hello|world', 'hello')
print(result)  # <re.Match object; span=(0, 5), match='hello'>
```

2. 문자열 범위 지정

- 1문자
    `[ ]` : 대괄호안의 문자 중 1문자
    `.`   : 꼭 1문자
    `?`   : 앞의 문자 0, 1 문자

- 반복자
    `*`   : 앞의 문자 0, 1회 이상 반복
    `+`   : 앞의 문자 1회 이상 반복
    `{ }` : 앞의 문자를 지정 반복 횟수만큼 반복

- [ ] 안에 들어갈 정규표현식
    `-`   : 범위 지정 - [a-z]
    `^`   : not - [^0-9] = \D
```python
result = re.findall('[0-9]', '1234')
print(result)  # ['1', '2', '3', '4']

result = re.findall('[0-9].', '1234')
print(result)  # ['12', '34']

result = re.findall('[0-9]?', '1234')
print(result)  # ['1', '2', '3', '4', '']

result = re.match('[0-9]*', '1234')
print(result)  # <re.Match object; span=(0, 4), match='1234'>

result = re.match('a+b', 'aab')
print(result)  # <re.Match object; span=(0, 3), match='aab'>

result = re.findall('(hello){2}', 'hellohellohelloworld')
print(result)  # ['hello']

result = re.match('[0-9]{3}-[0-9]{4}-[0-9]{4}','010-1000-1000')
print(result)  # <re.Match object; span=(0, 13), match='010-1000-1000'>

result = re.match('[^A-Z]+', 'Hello')
print(result)  # None
```

3. 문자열 위치 지정
    `^` : 문자열 시작에 매치
    `$` : 문자열 끝에 매치

```python
result = re.search('^[A-Z]+', 'Hello') 
print(result)  # <re.Match object; span=(0, 1), match='H'>

result = re.search('[0-9]+$', 'Hello1234') 
print(result)  # <re.Match object; span=(5, 9), match='1234'>
```

4. 탐닉

| Pattern | Matches |
|:--------|:--------|
| prev (?= next ) | prev if followed by next |
| prev (?! next ) | prev if not followed by next |
| (?<= prev ) next | next if preceded by prev |
| (?<! prev ) next | next if not preceded by prev |

```python
>>> re.findall('I (?=wish)', source)
['I ', 'I ']
```
And last, wish preceded by I:

```python
>>> re.findall('(?<=I) wish', source)
[' wish', ' wish']
```

5. 특수 문자

- `\d`: [0-9]와 같음. 모든 숫자
- `\D`: [^0-9]와 같음. 숫자를 제외한 모든 문자
- `\w`: [a-zA-Z0-9_]와 같음. 영문 대소문자, 숫자, 밑줄 문자
- `\W`: [^a-zA-Z0-9_]와 같음. 영문 대소문자, 숫자, 밑줄 문자를 제외한 모든 문자
- `\s`: [ \t\n\r\f\v]와 같음. 공백(스페이스), \t(탭) \n(새 줄, 라인 피드), \r(캐리지 리턴), \f(폼피드), \v(수직 탭)
- `\S`: [^ \t\n\r\f\v]와 같음 = [^\s]



6. group

- ()로 묶어 그룹지운다.

```python
m = re.match('([0-9]+) ([0-9]+)', '10 295')
print(m.groups())  # ('10', '295')
print(m.group(0))  # 10 295
print(m.group(1))  # 10
```
- 그룹이름 지정   
(?P<이름>정규표현식)

```python
m = re.match('(?P<func>[a-zA-Z_][a-zA-Z0-9_]+)\((?P<arg>\w+)\)', 'print(1234)')
g1 = m.group('func')    
print(g1)  # 'print'
g2 = m.group('arg')     
print(g2)  # '1234'
```

7. 교체 함수를 이용한 sub구현

- 교체함수(매치객체) 정의
- re.sub('패턴', 교체함수, '문자열', 바꿀횟수)

```python
def multiple10(m):        # 매개변수로 매치 객체를 받음
    n = int(m.group())    # 매칭된 문자열을 가져와서 정수로 변환
    return str(n * 10)    # 숫자에 10을 곱한 뒤 문자열로 변환해서 반환

result = re.sub('[0-9]+', multiple10, '1 2 Fizz 4 Buzz Fizz 7 8')
print(result) # '10 20 Fizz 40 Buzz Fizz 70 80'

result = re.sub('[0-9]+', lambda m: str(int(m.group()) * 10),
       '1 2 Fizz 4 Buzz Fizz 7 8')
print(result)
```

8. 그룹 재이용 : 그룹 카운터는 1부터 시작

- \\숫자  = \\g<숫자>
- \\g<이름>

```python
result = re.sub('([a-z]+) ([0-9]+)', '\\2 \\1 \\2 \\1', 'hello 1234')    # 그룹 2, 1, 2, 1 순으로 바꿈
print(result) # '1234 hello 1234 hello'

result = re.sub('({\s*)"(\w+)":\s*"(\w+)"(\s*})', '<\\2>\\3</\\2>', '{ "name": "james" }')
print(result) # '<name>james</name>'

result = re.sub('({\s*)"(?P<key>\w+)":\s*"(?P<value>\w+)"(\s*})', '<\\g<key>>\\g<value></\\g<key>>', '{ "name": "james" }')
'<name>james</name>'
print(result)  # <name>james</name>
```

9. 사용 예

```python
import re
exp = '^[a-zA-Z0-9+-_.]+@[a-zA-Z0-9-]+\.[a-z0-9-.]+$'
p = re.compile(exp)
emails = [
    'python@mail.example.com',
    'python+kr@example.com',  # 올바른 형식
    'python-dojang@example.co.kr',
    'python_10@example.info',  # 올바른 형식
    'python.dojang@e-xample.com',  # 올바른 형식
    '@example.com',
    'python@example',
    'python@example-com'
]  # 잘못된 형식

for email in emails:
    print(p.match(email) != None, end=' ')
```
```python
import re

exp = '^https?://[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+/[a-zA-Z0-9-_/.?=]*'  
p = re.compile(exp)

url = input()
print(p.match(url) != None)
```


