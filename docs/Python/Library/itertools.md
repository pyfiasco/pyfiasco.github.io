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

