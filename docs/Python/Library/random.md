---
layout: default
title: random
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

### Random
```python
from random import choice, sample, randint, randrange, random
result = choice([23, 9, 46, 'bacon', 0x123abc]),choice( ('a', 'one', 'and-a', 'two') ),choice(range(100)),choice('alphabet')
print(result ) # ('bacon', 'and-a', 23, 'l')

result = sample([23, 9, 46, 'bacon', 0x123abc], 3),sample(('a', 'one', 'and-a', 'two'), 2),sample(range(100), 4),sample('alphabet', 7)
print(result ) # (['bacon', 23, 1194684], ['two', 'and-a'], [38, 6, 8, 22], ['b', 'e', 'p', 'l', 't', 'a', 'a'])

result = randint(38, 74), randint(38, 74), randint(38, 74)
print(result ) # (39, 48, 48)

result = randrange(38, 74),randrange(38, 74, 10),randrange(38, 74, 10)
print(result ) # (45, 38, 48)

result = random(),random(),random(),
print(result ) # (0.048742540186274774, 0.7857409864362399, 0.5730595188281751)
```