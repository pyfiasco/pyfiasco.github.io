---
layout: default
title: Code Sample

has_children: true
---

# Code Sample

## time측정

```python
from time import time
from functools import reduce


def profile(func):
    def wrapper(n):
        begin = time()    # 함수가 시작된 시간
        r = func(n)
        end = time()      # 함수가 끝난 시간
        print('실행 시간: {0:.3f}초'.format(end - begin))    # 끝난 시간에서 시작된 시간을 빼면
        return r                                             # 실행 시간
    return wrapper


@profile
def factorial(n):
    return reduce(lambda x, y: x * y, range(1, n + 1))


factorial(10000)    # 숫자가 매우 커서 반환값 출력은 생략
```


