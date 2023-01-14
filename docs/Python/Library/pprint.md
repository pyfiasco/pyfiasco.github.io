---
layout: default
title: pprint
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
```python
from pprint import pprint
from collections import OrderedDict
quotes = OrderedDict([('Moe', 'A wise guy, huh?'),
                      ('Larry', 'Ow!'),
                      ('Curly', 'Nyuk nyuk!'),
                      ])
print(quotes)  
# OrderedDict([('Moe', 'A wise guy, huh?'), ('Larry', 'Ow!'), ('Curly', 'Nyuk nyuk!')])

result = pprint(quotes) # 정렬 출력
print(result)           # none
```

```python
from pprint import pprint

a = [[10, 20], [30, 40], [50, 60]]
pprint(a, indent = 4,width=20)
```

