---
#title: Automated Deployment
title: palindrome & N-gram
parent: code_sample
---

# palindrome

## 방법 1
```python
def  palindrome(word):    
    is_palindrome = True                 # 회문 판별값을 저장할 변수, 초깃값은 True
    for i in range(len(word) // 2):      # 0부터 문자열 길이의 절반만큼 반복
        if word[i] != word[-1 - i]:      # 왼쪽 문자와 오른쪽 문자를 비교하여 문자가 다르면
            is_palindrome = False        # 회문이 아님
            break
    
    return is_palindrome                 # 회문 판별값 출력

for i in ["level", "SOS", "rotator", "nurses run"]:
    print(i,":", palindrome(i))

```

## 방법 2
```python
def  palindrome(word):    
    if word == word[::-1]:
        return True 
    else:
        return False


for i in ["level", "SOS", "rotator", "nurses run"]:
    print(i,":", palindrome(i))
```

## 방법 3

- reversed함수의 반환형은 reversed object
- sorted함수의 반환형은 list object

```python
def  palindrome(word):    
    if word == ''.join(list(reversed(word))): 
        return True 
    else:
        return False


for i in ["level", "SOS", "rotator", "nurses run"]:
    print(i,":", palindrome(i))
```

## 방법 4 - 재귀함수 이용

```python
def is_palindrome(word):
    if len(word) < 2:
        return True
    if word[0] != word[-1]:
        return False
    return is_palindrome(word[1:-1])
                                    
 
print(is_palindrome('hello'))
print(is_palindrome('level'))
```


## 방법 5

```python
from string import punctuation
with open('words.txt','r') as f:
    source = f.read().split()  
    for i in source:
        test = i.strip(punctuation + ' ' + '')
        if test == test[::-1]:
            print(test)
```

# 방법6 - deque이용

```python
from collections import deque
def palindrome(word):
    dq = deque(word)
    while len(dq) > 1:
        if dq.popleft() != dq.pop():
            return False
    return True

result = palindrome('a'), palindrome('racecar'),palindrome(''),palindrome('radar'),palindrome('halibut')
print(result)  # (True, True, True, True, False)
```

# N-gram

## 방법 1
```python
def  ngram(word,length=2):  
    L=[]  
    for i in range(len(word)+1-length):
        s =''
        for j in range(length):
            s +=word[i+j]
        L.append(s)
    return L

text = 'this is python script'
print(ngram(text,4))
```
## 방법 2 - zip이용
```python
def  ngram(word,length=2):     
    L = list(zip(*[ word[i:] for i in range(length)]))
    result =[]
    for i in L:
        result.append(''.join(i))
    
    return result


text = 'this is python script'
result = ngram(text,length=5)
print(result)
```

## 방법 3 - 단어 단위 N-gram

```python
n = int(input())
text = input()
words = text.split() 
if (len(words) < n ):
    print('wrong')
else:
    n_gram = zip(*[ words[i:] for i in range(n)])                                  
    for i in n_gram:
        print(i)
```

