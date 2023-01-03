---
layout: default
title: date / time Module
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

# datetime 모듈
```python
from datetime import date
halloween = date(2019, 10, 31)
print(halloween) # datetime.date(2019, 10, 31)
print(halloween.day) # 31

now = date.today()
print(now)         # 오늘 날짜 출력

from datetime import timedelta
delta = timedelta(days=1)
tomorrow = now + delta
print('now : %s, tomorrow : %s'%(now,tomorrow))
print(now + 17*delta)  # 17일 후

# 타임 다루기
from datetime import time
noon = time(12, 0, 0)
print(noon) # datetime.time(12, 0)
print(noon.hour) # 12

from datetime import datetime
some_day = datetime(2019, 1, 2, 3, 4, 5, 6) #마지막인수 - 마이크로초
print(some_day)  # datetime.datetime(2019, 1, 2, 3, 4, 5, 6)
iso = some_day.isoformat()  # datetime자료형 -> 인식 가능 하게
print(iso) # 2019-01-02T03:04:05.000006

now = datetime.now()
print(now)  # 2022-12-30 22:09:49.004540
print(now.year) # 2022

d = some_day.date() # date부분만 추출
print(d)            # 2019-01-02
s = some_day.time() # time부분만 추출
print(s) # 03:04:05.000006

con = datetime.combine(d,s) # date, time -> datetime으로
print(con)                  # 2019-01-02 03:04:05.000006
```
## time module
```python
import time
now = time.time() # 현재시간
print(now)  # 1672408363.7341585

# epoch -> 문자열
t1 = time.ctime(now)
print(t1)  # Fri Dec 30 22:54:14 2022


# struct_time - 인수 생략 시 현재기준
t2 = time.localtime(now)     # 시스템 표준 시간대로 나타냄
t3 = time.gmtime(now)        # UTC(절대시간)로 나타냄
print(t2)
print(t3)
print(t3[0])  # 2022    - 인덱스 사용 가능
# time.struct_time(tm_year=2022, tm_mon=12, tm_mday=30, tm_hour=22, tm_min=59, tm_sec=3, tm_wday=4, tm_yday=364, tm_isdst=0)
# tm_wday : 요일
# tm_yday : 년일자(일/365)
# tm_isdst: 일광시간 절약제 (0:아니오, 1:예, -1: 모름)

t4 = time.mktime(t2) # struct_time -> epoch
print(t4)  # 1672409675.0

<div class="code-example" markdown="1">

| Format string | Date/time unit | Range        |
|:--------------|:---------------|:-------------|
| %Y            | year           | 1900 -...    |
| %m            | month          | 01 - 12      |
| %B            | month name     | January, ... |
| %b            | month abbrev   | Jan, ...     |
| %d            | day of month   | 01 - 31      |
| %A            | weekday name   | Sunday, ...  |
| a             | weekday abbrev | Sun, ...     |
| %H            | hour (24 hr)   | 00 - 23      |
| %I            | hour (12 hr)   | 01 - 12      |
| %p            | AM/PM          | AM, PM       |
| %M            | minute         | 00 - 59      |
| %S            | second         | 00 - 59      |

</div>

## 날짜 시간 읽고/쓰기
# strftime함수 이용

import time
fmt = "It's %A, %B %d, %Y, local time %I:%M:%S%p"
t = time.localtime()
print(t)
# time.struct_time(tm_year=2022, tm_mon=12, tm_mday=30, tm_hour=23, tm_min=32, tm_sec=58, tm_wday=4, tm_yday=364, tm_isdst=0)
result = time.strftime(fmt,t)
print(result)  # It's Friday, December 30, 2022, local time 11:35:17PM

# 시간부분 무시
from datetime import date
t1 = date.today()
result = t1.strftime(fmt)
print(result)  # It's Friday, December 30, 2022, local time 12:00:00AM

# 날짜부분 무시
from datetime import time
t2 = time(10,1,1)
result = t2.strftime(fmt)
print(result)  #It's Monday, January 01, 1900, local time 10:01:01AM

import time
fmt = "%Y-%m-%d"
t3 = time.strptime("2019-01-29", fmt)
print(t3)
# time.struct_time(tm_year=2019, tm_mon=1, tm_mday=29, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=1, tm_yday=29, tm_isdst=-1)

fmt = "%Y%m%d"
t4 = time.strptime("20190129", fmt)
print(t4)
# time.struct_time(tm_year=2019, tm_mon=1, tm_mday=29, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=1, tm_yday=29, tm_isdst=-1)

# 할로윈 출력
import locale
from datetime import date
halloween = date(2019, 10, 31)
for lang_country in ['en_us', 'fr_fr', 'de_de', 'es_es', 'is_is',]:
    locale.setlocale(locale.LC_TIME, lang_country)
    result = halloween.strftime('%A, %B %d')
    print(result.encode('utf-8', 'ignore').decode('utf-8', 'replace'))
'''
Thursday, October 31
jeudi, octobre 31
Donnerstag, Oktober 31
jueves, octubre 31
fimmtudagur, oktber 31
'''

# lang_country에 대해
import locale
names = locale.locale_alias.keys()
print(names)   # 전체 지역코드 반환 (딕셔너리)  : 2자리 언어 코드_2자리 국가 코드
good_names = [name for name in names if \
len(name) == 5 and name[2] == '_']
r1 = good_names[:5]
print(r1)  # ['a3_az', 'aa_dj', 'aa_er', 'aa_et', 'af_za']
de = [name for name in good_names if name.startswith('ko')]
print(de) # ['de_at', 'de_be', 'de_ch', 'de_de', 'de_it', 'de_lu']
```

## 기타 모듈

- [arrow](https://arrow.readthedocs.io/en/latest/) : Combines many date and time functions with a simple API

- [dateutil](http://labix.org/python-dateutil) : Parses almost any date format and handles relative dates and times well

- [iso8601](https://pypi.org/project/iso8601/) : Fills in gaps in the standard library for the ISO8601 format

- [fleming](https://github.com/ambitioninc/fleming) : Many time zone functions

- [maya](https://github.com/kennethreitz/maya) : Intuitive interface to dates, times, and intervals

- [dateinfer](https://github.com/jeffreystarr/dateinfer)   : Guesses the right format strings from date/time strings