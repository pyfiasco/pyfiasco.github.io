---
layout: default
title: 9장 Functions
parent: Basic
grand_parent: Python
nav_order: 9
---

# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

**CHAPTER 9**
**Functions**

A function can take any number and type of input `parameters` and return any number and type of output `results`.

You can do two things with a function:

- `Define` it, with zero or more parameters
- `Call` it, and get zero or more results


### Define a Function with def

To define a Python function, you type `def`, the function name, parentheses enclosing

any input `parameters` to the function, and then finally, a colon (:). 

Here’s the simplest Python function:

```python
>>> def do_nothing():
... pass
```

```
>>> print (do_nothing())
None
```

### Call a Function with Parentheses

```python
>>> do_nothing()
>>>
```

### Arguments and Parameters

The values you pass into the function when you call it are known as `arguments`. When

you call a function with arguments, the values of those arguments are copied to their

corresponding `parameters` inside the function.

{: .note}
> Saying it another way: they’re called <code> rguments </code> outside of the func‐
tion, but <code> parameters </code> inside.


<br>
#### None Is Useful

`None` 은 value,type 없이 공간만 차지하는 파이션의 특별한 값이다, bool자료형으로 평가시 `false` 이다.   
> bool자료형 false인 zero-valued integers(0),  floats(0.0), empty strings (''), lists ([]), tuples ((,)), dictionaries ({}), and sets(set())은 false로 평가되지만 `None`은 아니다.   

> bool `false`와 `None`을 구별하기 위해 `is` operator를 사용한다.

Here’s an example:

```python
>>> thing = None
>>> if thing is None:
...     print ("It's nothing")
... else :
...     print ("It's something")
...
It's nothing
```

```python
>>> def whatis(thing):
...     if thing is None:
...         print (thing, "is None")
...     elif thing:
...         print (thing, "is True")
...     else :
...         print (thing, "is False")
>>> whatis(0)
0 is False
>>> whatis(0.0)
0.0 is False
>>> whatis('')
is False
>>> whatis("")
is False
>>> whatis('''''')
is False
>>> whatis(())
() is False
>>> whatis([])
[] is False
>>> whatis({})
{} is False
>>> whatis(set())
set() is False
>>> whatis(0.00001)
1e-05 is True
>>> whatis([0])
[0] is True
>>> whatis([''])
[''] is True
>>> whatis(' ')
 is True
```
#### Positional Arguments

The most familiar types of arguments are `positional arguments`, whose values are copied to their orresponding parameters in order.

This function builds a dictionary from its positional input arguments and returns it:

```python
>>> def menu(wine, entree, dessert):
...     return {'wine': wine, 'entree': entree, 'dessert': dessert}
...
>>> menu('chardonnay', 'chicken', 'cake')
{'wine': 'chardonnay', 'entree': 'chicken', 'dessert': 'cake'}
```

#### Keyword Arguments

To avoid positional argument confusion, you can specify arguments by the names of their corresponding parameters, even in a different order from their definition in the function:

```python
>>> menu(entree='beef', dessert='bagel', wine='bordeaux')
{'wine': 'bordeaux', 'entree': 'beef', 'dessert': 'bagel'}
```
You can mix positional and keyword arguments. Let’s specify the wine first, but use keyword arguments for the entree and dessert:

```python
>>> menu('frontenac', dessert='flan', entree='fish')
{'wine': 'frontenac', 'entree': 'fish', 'dessert': 'flan'}
```
If you call a function with both positional and keyword arguments, the positional arguments need to come first.

#### Specify Default Parameter Values

You can specify default values for parameters. The default is used if the caller does not provide a corresponding argument. This bland-sounding feature can actually be quite useful. Using the previous example:

```python
>>> def menu(wine, entree, dessert='pudding'):
...     return {'wine': wine, 'entree': entree, 'dessert': dessert}
```
This time, try calling menu() without the dessert argument:

```python
>>> menu('chardonnay', 'chicken')
{'wine': 'chardonnay', 'entree': 'chicken', 'dessert': 'pudding'}
```
If you do provide an argument, it’s used instead of the default:

```python
>>> menu('dunkelfelder', 'duck', 'doughnut')
{'wine': 'dunkelfelder', 'entree': 'duck', 'dessert': 'doughnut'}
```
<br>

{: .note}
> Default parameter values은 실행될 때가 아니라 `정의`될 때 계산됩니다.    
> Mutable data type(list,dictionary )는 default parameter로 사용하지 말라!!!.

다음에서 빈 list에 하나의 데이터를 더하여 하나의 요소를 갖은 list를 반환하기를 원하지만 결과는 그렇지 않다.
두번째 호출에 이전 호출의 결과가 참조된다.

```python
>>> def buggy(arg, result=[]):
...     result.append(arg)
...     print (result)

>>> buggy('a')
['a']
>>> buggy('b') # expect ['b']
['a', 'b']
```
수정 :

```python
>>> def works(arg):
...     result = []
...     result.append(arg)
...     return result

>>> works('a')
['a']
>>> works('b')
['b']
```
해결책 :

```python
>>> def nonbuggy(arg, result=None):
...     if result is None:
...         result = []
...     result.append(arg)
...     print (result)

>>> nonbuggy('a')
['a']
>>> nonbuggy('b')
['b']
```

#### Explode/Gather Positional Arguments with *

Python 프로그램는 포인터가 없다. parameter의 asterisk (`*`)는 positional arguments을 tuple화 한다.

```python
>>> def print_args(*args):
...     print ('Positional tuple:', args)
...
```
```python
# 인자 전달이 없는 경우 :
>>> print_args()
Positional tuple: ()

# 전달된 인자는 tuple화 :
>>> print_args(3, 2, 1, 'wait!', 'uh...')
Positional tuple: (3, 2, 1, 'wait!', 'uh...')
```
```python
# positional arguments가 할당된 나머지가 *args에 할당 :
>>> def print_more(required1, required2, *args):
...     print ('Need this one:', required1)
...     print ('Need this one too:', required2)
...     print ('All the rest:', args)
...
>>> print_more('cap', 'gloves', 'scarf', 'monocle', 'mustache wax')
Need this one: cap
Need this one too: gloves
All the rest: ('scarf', 'monocle', 'mustache wax')
```
Summarizing:

- You can pass positional argument to a function, which will match them inside to positional parameters. This is what you’ve seen so far in this book.
- You can pass a tuple argument to a function, and inside it will be a tuple parameter. This is a simple case of the preceding one.
- You can pass positional arguments to a function, and gather them inside as the parameter `*args`, which resolves to the tuple `args`. This was described in this section.
- You can also “explode” a tuple argument called `args` to positional parameters `*args` inside the function, which will be regathered inside into the tuple parameter `args`:    

```python
>>> print_args(2, 5, 7, 'x')
Positional tuple: (2, 5, 7, 'x')
```

```python
>>> args = (2,5,7,'x')
>>> print_args(args)
Positional tuple: ((2, 5, 7, 'x'),)
>>> print_args(*args)
Positional tuple: (2, 5, 7, 'x')
```
You can only use the * syntax in a function call or definition:

```python
>>> *args
File "<stdin>", line 1
SyntaxError: can't use starred expression here
```
So:

- Outside the function, `*args` explodes the tuple `args` into comma-separated positional parameters.
- Inside the function, `*args` gathers all of the positional arguments into a single `args` tuple. You could use the names `*params` and `params`, but it’s common practice to use `*args` for both the outside argument and inside parameter.

Readers with synesthesia might also faintly hear `*args` as *puff-args* on the outside and *inhale-args* on the inside, as values are either exploded or gathered.

#### Explode/Gather Keyword Arguments with **

You can use two asterisks (`**`) to group keyword arguments into a dictionary, where the argument names are the keys, and their values are the corresponding dictionary values. The following example defines the function print_kwargs() to print its keyword arguments:

```python
>>> def print_kwargs(**kwargs):
...     print ('Keyword arguments:', kwargs)
...
```
Now try calling it with some keyword arguments:

```python
>>> print_kwargs()
Keyword arguments: {}
>>> print_kwargs(wine='merlot', entree='mutton', dessert='macaroon')
Keyword arguments: {'dessert': 'macaroon', 'wine': 'merlot',
'entree': 'mutton'}
```
Inside the function, kwargs is a dictionary parameter.

{: .note}
> Argument order is:
- Required positional arguments
- Optional positional arguments (*args)
- Optional keyword arguments (**kwargs)

As with args, you don’t need to call this keyword argument kwargs, but it’s common usage.

The ** syntax is valid only in a function call or definition:

```python
>>> **kwparams
File "<stdin>", line 1
**kwparams
^
SyntaxError: invalid syntax
```
Summarizing:

- You can pass keyword arguments to a function, which will match them inside to keyword parameters. This is what you’ve seen so far.
- You can pass a dictionary argument to a function, and inside it will be dictionary parameters. This is a simple case of the preceding one.
- You can pass one or more keyword arguments (*name=value*) to a function, and gather them inside as `**kwargs`, which resolves to the dictionary parameter called `kwargs`. This was described in this section.
- Outside a function, `**kwargs` *explodes* a dictionary `kwargs` into *name=value* arguments.
- Inside a function, `**kwargs` *gathers* `name=value` arguments into the single dictionary parameter `kwargs`.

If auditory hallucinations help, imagine a puff for each asterisk exploding outside the function, and a little inhaling sound for each one gathering inside.

#### Keyword-Only Arguments

It’s possible to pass in a keyword argument that has the same name as a positional parameter, probably not resulting in what you want. Python 3 lets you specify *keyword-only arguments*. As the name says, they must be provided as *name=value*, not positionally as *value*. The single `*` in the function definition means that the following parameters `start` and `end` must be provided as named arguments if we don’t want their default values:

```python
>>> def print_data(data, *, start=0, end=100):
...     result=[]
...     for value in (data[start:end]):
...         result.append(value)
...     print (*value)

>>> data = ['a', 'b', 'c', 'd', 'e', 'f']
>>> print_data(data)
a b c d e f
>>> print_data(data, start=4)
e f
>>> print_data(data, end=2)
a b

```
#### Mutable and Immutable Arguments

{: .note}
> - Remember that if you assigned the same list to two variables, you could change it by using either one? And that you could not if the variables both referred to something like an integer or a string? 
> - That was because the list was mutable and the integer and string were immutable.
> - You need to watch for the same behavior when passing arguments to functions. If an argument is mutable, its value can be changed from inside the function via its corresponding parameter:

```python
>>> outside = ['one', 'fine', 'day']
>>> def mangle(arg):
...     arg[1] = 'terrible!'
...
>>> outside
['one', 'fine', 'day']
>>> mangle(outside)
>>> outside
['one', 'terrible!', 'day']
```
It’s good practice to, uh, not do this.


### Docstrings

Readability counts, the Zen of Python verily saith. You can attach documentation to a function definition by including a string at the beginning of the function body. This is the function’s docstring:

```python
>>> def echo(anything):
...     'echo returns its input argument'
...     return anything
```
You can make a docstring quite long, and even add rich formatting if you want:

```python
def print_if_true(thing, check):
    '''
    Prints the first argument if a second argument is true.
    The operation is:
        1. Check whether the *second* argument is true.
        2. If it is, print the *first* argument.
    '''
    if check:
        print(thing)
```

<font color='red-300'>To print a function’s docstring, call the Python `help()` function. </font>Pass the function’s name to get a listing of arguments along with the nicely formatted docstring:

```python
>>> help(echo)
Help on function echo in module __main__:

echo(anything)
echo returns its input argument
```
If you want to see just the raw docstring, without the formatting:

```python
>>> print (echo.__doc__)
echo returns its input argument
```
<font color='red-300'>That odd-looking `__doc__` is the internal name of the docstring as a variable within the function.</font> Double underscores (aka dunder in Python-speak) are used in many places to name Python internal variables, because programmers are unlikely to use them in their own variable names.

### Functions Are First-Class Citizens

I’ve mentioned the Python mantra, everything is an object. This includes numbers, strings, tuples, lists, dictionaries—and functions, as well. Functions are first-class citizens in Python. You can assign them to variables, use them as arguments to other functions, and return them from functions. This gives you the capability to do some things in Python that are difficult-to-impossible to carry out in many other languages.

To test this, let’s define a simple function called answer() that doesn’t have any arguments; it just prints the number 42 :

```python
>>> def answer():
... print (42)
```
If you run this function, you know what you’ll get:

```python
>>> answer()
42
```
Now let’s define another function named run_something. It has one argument called func, a function to run. Once inside, it just calls the function:

```python
>>> def run_something(func):
... func()
```
If we pass answer to run_something(), we’re using a function as data, just as with anything else:

```python
>>> run_something(answer)
42
```

{: .important}
> Notice that you passed answer, not answer(). In Python, those parentheses mean *call this function*. With no parentheses, Python just treats the function like any other object. That’s because, like everything else in Python, it is an `object`:

```python
>>> type(run_something)
<class 'function'>
```
Let’s try running a function with arguments. Define a function add_args() that prints the sum of its two numeric arguments, arg1 and arg2:

```python
>>> def add_args(arg1, arg2):
... print (arg1 + arg2)
```
And what is add_args()?

```python
>>> type(add_args)
<class 'function'>
```
At this point, let’s define a function called run_something_with_args() that takes three arguments:

func
    The function to run
arg1
    The first argument for func
arg2
    The second argument for func


```python
>>> def run_something_with_args(func, arg1, arg2):
... func(arg1, arg2)
```
When you call run_something_with_args(), the function passed by the caller is assigned to the func parameter, whereas arg1 and arg2 get the values that follow in the argument list. Then, running func(arg1, arg2) executes that function with those arguments because the parentheses told Python to do so.

Let’s test it by passing the function name add_args and the arguments 5 and 9 to run_something_with_args():

```python
>>> run_something_with_args(add_args, 5, 9)
14
```
Within the function run_something_with_args(), the function name argument add_args was assigned to the parameter func, 5 to arg1, and 9 to arg2. This ended up running:

```python
add_args(5, 9)
```
You can combine this with the *args and **kwargs techniques.

Let’s define a test function that takes any number of positional arguments, calculates their sum by using the sum() function, and then returns that sum:

```python
>>> def sum_args(*args):
... return sum(args)
```
I haven’t mentioned sum() before. It’s a built-in Python function that calculates the sum of the values in its iterable numeric (int or float) argument.

Let’s define the new function run_with_positional_args(), which takes a function and any number of positional arguments to pass to it:

```python
>>> def run_with_positional_args(func, *args):
... return func(*args)
```
Now go ahead and call it:

```python
>>> run_with_positional_args(sum_args, 1, 2, 3, 4)
10
```
You can use functions as elements of lists, tuples, sets, and dictionaries. Functions are immutable, so you can also use them as dictionary keys.

### **Inner Functions**

 함수 내에서 함수를 정의할 수 있습니다.

```python
>>> def outer(a, b):
...     def inner(c, d):
...         return c + d
...     return inner(a, b)
>>>
>>> outer(4, 7)
11
```
<!-- An inner function can be useful when performing some complex task more than once within another function, to avoid loops or code duplication. For a string example, this inner function adds some text to its argument: -->
내부 함수는 루프나 코드 중복을 피하기 위해 다른 함수 내에서 복잡한 작업을 두 번 이상 수행할 때 유용할 수 있습니다.    
문자열 예제의 경우 이 내부 함수는 인수에 일부 텍스트를 추가합니다.


```python
>>> def knights(saying):
...     def inner(quote):
...         return "We are the knights who say: '%s'" % quote
...     return inner(saying)
>>> knights('Ni!')
"We are the knights who say: 'Ni!'"
```

#### **Closures**

<!-- An inner function can act as a closure. This is a function that is dynamically generated by another function and can both change and remember the values of variables that were created outside the function.

The following example builds on the previous knights() example. Let’s call the new one knights2(), because we have no imagination, and turn the inner() function into a closure called inner2(). Here are the differences: -->

내부 함수는 `클로저` 역할을 할 수 있습니다. 이것은 다른 함수에 의해 동적으로 생성되는 함수이며 함수 외부에서 생성된 변수의 값을 변경하고 기억할 수 있습니다.   
다음 예제는 이전 knights() 예제를 기반으로 합니다. 차이점은 다음과 같습니다.

- inner2()는 argument가 아닌 외부함수의 변수를 직접 사용한다.    
- knights2()는 내부함수를 호출하지 않고 함수이름을 반환한다. 

```python
>>> def knights2(saying):
...     def inner2():
...         return "We are the knights who say: '%s'" % saying
...     return inner2
...
>>> a = knights2('Duck')
>>> b = knights2('Hasenpfeffer')

>>> type(a)
<class 'function'>

# 함수 생성시 전달된 외부 인수를 기억하고 있다.
>>> a()
"We are the knights who say: 'Duck'"
>>> b()
"We are the knights who say: 'Hasenpfeffer'"
```

lambda함수를 내부함수로 자주 사용하라!!!

```python
def calc():
    a = 3
    b = 5
    return lambda x: a * x + b  # 람다 표현식을 반환


c = calc()
print(c(1), c(2), c(3), c(4), c(5))  # 8 11 14 17 20
```

카운터 구현

```python
def counter():
    i = 0
    def count():
        nonlocal i
        i+=1
        print('counter:',i)
    return count

c = counter()
for i in range(10):
    c()
```

### Anonymous Functions: lambda

A Python lambda function is an anonymous function expressed as a single statement.

You can use it instead of a normal tiny function.

To illustrate it, let’s first make an example that uses normal functions. To begin, let’s define the function edit_story(). Its arguments are the following:

- words—a list of words
- func—a function to apply to each word in words

```python
>>> def edit_story(words, func):
... for word in words:
... print (func(word))
```
Now we need a list of words and a function to apply to each word. For the words, here’s a list of (hypothetical) sounds made by my cat if he (hypothetically) missed one of the stairs:

```python
>>> stairs = ['thud', 'meow', 'thud', 'hiss']
```
And for the function, this will capitalize each word and append an exclamation point, perfect for feline tabloid newspaper headlines:

```python
>>> def enliven(word): # give that prose more punch
... return word.capitalize() + '!'
```
Mixing our ingredients:

```python
>>> edit_story(stairs, enliven)
Thud!
Meow!
```

```python
Thud!
Hiss!
```
Finally, we get to the lambda. The enliven() function was so brief that we could replace it with a lambda:

```python
>>> edit_story(stairs, lambda word: word.capitalize() + '!')
Thud!
Meow!
Thud!
Hiss!
```
A lambda has zero or more comma-separated arguments, followed by a colon (:), and then the definition of the function. We’re giving this lambda one argument, word.

You don’t use parentheses with lambda as you would when calling a function created with def.

Often, using real functions such as enliven() is much clearer than using lambdas.

Lambdas are mostly useful for cases in which you would otherwise need to define many tiny functions and remember what you called them all. In particular, you can use lambdas in graphical user interfaces to define callback functions; see Chapter 20

for examples.

### Generators
{: .text-red-100}

A generator is a Python sequence creation object. With it, you can iterate through potentially huge sequences without creating and storing the entire sequence in memory at once. Generators are often the source of data for iterators. If you recall, we already used one of them, range(), in earlier code examples to generate a series of integers. In Python 2, range() returns a list, which limits it to fit in memory. Python 2 also has the generator xrange(), which became the normal range() in Python 3.

This example adds all the integers from 1 to 100:

```python
>>> sum(range(1, 101))
5050
```
<!-- Every time you iterate through a generator, it keeps track of where it was the last time it was called and returns the next value. This is different from a normal function, which has no memory of previous calls and always starts at its first line with the same state. -->
`gnerator`는 순회할 때마다 마지막으로 호출된 항목을 기억하고 다음 값을 반환한다.

#### Generator Functions

If you want to create a potentially large sequence, you can write a generator function.   
It’s a normal function, but it returns its value with a yield statement rather than return. Let’s write our own version of range():


```python
>>> def my_range(first=0, last=10, step=1):
...     number = first
...     while number < last:
...         yield number
...         number += step

>>> my_range
<function my_range at 0x10193e268>

>>> ranger = my_range(1, 5)
>>> ranger
<generator object my_range at 0x101a0a168>

>>> for x in ranger:
... print (x)

1
2
3
4

>>> for try_again in ranger:
... print (try_again)        # 다시 순회하지 않는다.
>>>
```

{: .note}
> generator는 1회만 순회한다. Lists, sets, strings, and dictionaries는 메모리에 존재한다. 그러나 generator는 해당 값을 즉석에서 생성하고 iterator를 통해 한 번에 하나씩 전달된다. generator는 모든 값을 기억하지 않으므로 generator를 다시 시작하거나 되돌릴 수 없다.

#### Generator Comprehensions

You’ve seen comprehensions for `lists`, `dictionaries`, and `sets`. A `**generator comprehension**` looks like those, but `is surrounded by parentheses` instead of square or curly brackets. It’s like a shorthand version of a generator function, doing the yield invisibly, and also returns a generator object:

```python
>>> genobj = (pair for pair in zip(['a', 'b'], ['1', '2']))
>>> genobj
<generator object <genexpr> at 0x10308fde0>
>>> for thing in genobj:
... print (thing)

('a', '1')
('b', '2')
```
### Decorators
{: .text-red-100}

가끔 소스코드를 변화하지 않고 존재하는 함수를 수정하기를 원한다. 일반적인 예는 함수에 전달된 인수를 보기 위해 debugging statement를 더하는 것이다.    
`decorator`는 하나의 함수를 취해서 또 다른 함수를 반환하는 함수다.    

Let’s dig into our bag of Python tricks and use the following:

- *args and **kwargs
- Inner functions
- Functions as arguments

document_it() 함수는 다음과 같이 데커레이터를 정의한다.    

- 함수이름과 인수를 출력한다.
- 인수로 함수를 실행한다.
- 결과를 출력한다.
- 수정된 함수를 사용하도록 반환한다.

Here’s what the code looks like:

```python
>>> def document_it(func):
...     def new_function(*args, **kwargs):
...         print ('Running function:', func.__name__)
...         print ('Positional arguments:', args)
...         print ('Keyword arguments:', kwargs)
...         result = func(*args, **kwargs)
...         print ('Result:', result)
...         return result
...     return new_function
```
Whatever func you pass to document_it(), you get a new function that includes the extra statements that document_it() adds. A decorator doesn’t actually have to run any code from func, but document_it() calls func partway through so that you get the results of func as well as all the extras.

So, how do you use this? You can apply the decorator manually:

```python
>>> def add_ints(a, b):
... return a + b
...
>>> add_ints(3, 5) # 8
```

```python
>>> cooler_add_ints = document_it(add_ints) # manual decorator assignment
>>> cooler_add_ints(3, 5)
Running function: add_ints
Positional arguments: (3, 5)
Keyword arguments: {}
Result: 8
8
```
As an alternative to the manual decorator assignment we just looked at, you can add @ _decorator_name_ before the function that you want to decorate:

```python
>>> @document_it
... def add_ints(a, b):
...     return a + b
...
>>> add_ints(3, 5)
Start function add_ints
Positional arguments: (3, 5)
Keyword arguments: {}
Result: 8
8
```
You can have more than one decorator for a function. Let’s write another decorator called square_it() that squares the result:

```python
>>> def square_it(func):
...     def new_function(*args, **kwargs):
...         result = func(*args, **kwargs)
...         return result * result
...     return new_function
...
```
The decorator that’s used closest to the function (just above the def) runs first and then the one above it. Either order gives the same end result, but you can see how the intermediate steps change:

```python
>>> @document_it
... @square_it
... def add_ints(a, b):
...     return a + b
...
>>> add_ints(3, 5)
Running function: new_function
Positional arguments: (3, 5)
Keyword arguments: {}
Result: 64
64
```
Let’s try reversing the decorator order:

```python
>>> @square_it
... @document_it
... def add_ints(a, b):
...     return a + b
```
```python
>>> add_ints(3, 5)
Running function: add_ints
Positional arguments: (3, 5)
Keyword arguments: {}
Result: 8
64
```
```python
def document_it(func):
    def new_function(*args, **kwargs):
        print ('Running function:', func.__name__)
        print ('Positional arguments:', args)
        print ('Keyword arguments:', kwargs)
        result = func(*args, **kwargs)
        print ('Result:', result)
        return result
    return new_function

def square_it(func):
    def new_func(*args, **kwargs):
        result = func(*args, **kwargs)
        return result * result
    return new_func


@document_it
@square_it
def add_ints(a, b):
    return a + b

result = add_ints(3, 5)
print("final:", result)
print("-"*10)


@square_it
@document_it
def add_ints(a, b):
    return a + b

result = add_ints(3,5)
print("final:",result)
```


### Namespaces and Scope

<!-- ```
Desiring this man’s art and that man’s scope
—William Shakespeare
```
A name can refer to different things, depending on where it’s used. Python programs

have various namespaces—sections within which a particular name is unique and

unrelated to the same name in other namespaces.

Each function defines its own namespace. If you define a variable called x in a main

program and another variable called x in a function, they refer to different things. But

the walls can be breached: if you need to, you can access names in other namespaces

in various ways.

The main part of a program defines the global namespace; thus, the variables in that

namespace are global variables.

You can get the value of a global variable from within a function: -->
name은 사용되는 위치에 따라 다른 항목을 참조할 수 있습니다.    
Python 프로그램에는 다양한 namespace가 있으며, 그 내에서 특정 이름이 고유하고 다른 namespace의 동일한 이름과 관련이 없는 섹션입니다.

각 함수는 자체 namespace를 정의합니다. 메인 프로그램에서 x라는 변수를 정의하고 함수에서 x라는 다른 변수를 정의하면 서로 다른 것을 참조합니다. 

프로그램의 주요 부분은 전역 이름 공간을 정의합니다. 따라서 해당 namespace의 변수는 전역 변수입니다.

함수 내에서 전역 변수의 값을 가져올 수 있습니다.

함수내에서 global 선언한 변수가 전역에 존재하지 않으면 지역변수로 전환된다.


```python
animal = 'fruitbat'
def print_global():
    print ('inside print_global:', animal)

print ('at the top level:', animal) # at the top level: fruitbat
print_global() # inside print_global: fruitbat
```
But if you try to get the value of the global variable and change it within the function, you get an error:

```python
def change_and_print_global():
    print ('inside change_and_print_global:', animal) # 지역변수 초기화 실패)
    animal = 'wombat'
    print ('after the change:', animal)

change_and_print_global() # 에러 발생
```

If you just change it, it changes a different variable also named animal, but this variable is inside the function:

```python
animal = 'fruitbat'
def change_local():
    animal = 'wombat'
    print ('inside change_local:', animal, id(animal))

change_local()  # inside change_local: wombat 1618131858544
print(animal, ':', id(animal))  # fruitbat : 1618131753520
```
<!-- What happened here? The first line assigned the string 'fruitbat' to a global variable named animal. The change_local() function also has a variable named animal, but that’s in its local namespace.

I used the Python function id() here to print the unique value for each object and prove that the variable animal inside change_local() is not the same as animal at the main level of the program.

To access the global variable rather than the local one within a function, you need to be explicit and use the global keyword (you knew this was coming: explicit is better than implicit): -->

함수 내의 로컬 변수가 아닌 전역 변수에 액세스하려면 명시 적이어야하며 `global` 키워드를 사용해야합니다 
- global변수 값 변경 시 필수

```python
animal = 'fruitbat'
def change_and_print_global():
    global animal
    animal = 'wombat'
    print ('inside change_and_print_global:', animal)

print(animal) # 'fruitbat'
change_and_print_global() # inside change_and_print_global: wombat
print(animal) # 'wombat'
```
<!-- If you don’t say global within a function, Python uses the local namespace and the variable is local. It goes away after the function completes. -->
함수 내에서 global이라고 말하지 않으면 Python은 로컬 namespace를 사용하고 변수는 local입니다. 함수가 완료되면 사라집니다.

{: .note}
> namespaces에 억세스하기:
> 
> - locals() : local namespace의 dictionary.( 전역에서 실행시 globals()기능 수행)
> - globals() : global namespace의 dictionary.


And here they are in use:

```python
>>> animal = 'fruitbat'
>>> def change_local():
... animal = 'wombat' # local variable
... print ('locals:', locals())
```
```python
>>> animal
'fruitbat'
>>> change_local()
locals: {'animal': 'wombat'}
>>> print ('globals:', globals()) # reformatted a little for presentation
globals: {'animal': 'fruitbat',
'__doc__': None,
'change_local': <function change_local at 0x1006c0170>,
'__package__': None,
'__name__': '__main__',
'__loader__': <class '_frozen_importlib.BuiltinImporter'>,
'__builtins__': <module 'builtins'>}
>>> animal
'fruitbat'
```
The local namespace within change_local() contained only the local variable animal. The global namespace contained the separate global variable animal and a number of other things.

### Uses of `_` and `__` in Names

Names that begin and end with two underscores (`__`) are reserved for use within Python, so you should not use them with your own variables. This naming pattern was chosen because it seemed unlikely to be selected by application developers for their own variables.

For instance, the name of a function is in the system variable `_function_` `.__name__`, and its documentation string is `_function_` `.__doc__`:

```python
>>> def amazing():
... '''This is the amazing function.
... Want to see it again?'''
... print ('This function is named:', amazing.__name__)
... print ('And its docstring is:', amazing.__doc__)
...
>>> amazing()
This function is named: amazing
And its docstring is: This is the amazing function.
Want to see it again?
```
As you saw in the earlier globals printout, the main program is assigned the special name `__main__`.


```
5 It’s like saying, “I wish I had a dollar for every time I wished I had a dollar.”
6 Another Python interview question. Collect the whole set!
```
### Recursion(재귀함수)

So far, we’ve called functions that do some things directly, and maybe call other functions. But what if a function calls itself? This is called `recursion`. Like an unbroken infinite loop with while or for, you don’t want infinite recursion. Do we still need to worry about cracks in the space-time continuum?

Python saves the universe again by raising an exception if you get too deep:

```python
>>> def dive():
... return dive()
...
>>> dive()
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
File "<stdin>", line 2, in dive
File "<stdin>", line 2, in dive
File "<stdin>", line 2, in dive
[Previous line repeated 996 more times]
RecursionError: maximum recursion depth exceeded
```
Recursion is useful when you’re dealing with “uneven” data, like lists of lists of lists.

Suppose that you want to “flatten” all sublists of a list, no matter how deeply nested.

A generator function is just the thing:

```python
>>> def flatten(lol):
...     for item in lol:
...         if isinstance(item, list):
...             for subitem in flatten(item):
...                 yield subitem
...         else :
...             yield item
...
>>> lol = [1, 2, [3,4,5], [6,[7,8,9], []]]
>>> flatten(lol)
<generator object flatten at 0x10509a750>
>>> list(flatten(lol))
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```
(Python 3.3 이상) `yield from` expression을 추가하여 제너레이터가 몇몇 작업을 다른 제너레이터에게 전달할 수 있다. 

```python
>>> def flatten(lol):
...     for item in lol:
...         if isinstance(item, list):
...             yield from flatten(item)
...         else :
...             yield item
```
```python
>>> lol = [1, 2, [3,4,5], [6,[7,8,9], []]]
>>> list(flatten(lol))
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

**피보나치수**

```python
def fib(n):
    if n>=2:
        return fib(n-1) + fib(n-2)
    elif n == 1:
        return 1
    elif n ==0:
        return 0        


n = int(input())
print(fib(n))
```

### Async Functions
{: .text-red-100}

The keywords `async` and `await` were added to Python 3.5 to define and run asynchronous functions. They’re:

- Relatively new
- Different enough to be harder to understand
- Will become more important and better known over time

For these reasons, I’ve moved discussion of these and other async topics to `Appendix C`.

For now, you need to know that if you see `async` *before the def line for a function*, it’s an asynchronous function. Likewise, if you see `await` *before a function call*, that function is asynchronous.

The main difference between asynchronous and normal functions is that async ones can “제어를 넘겨주는 것” rather than running to completion.

### **Exceptions**

[Exception 계층구조](https://docs.python.org/3/library/exceptions.html#exception-hierarchy)

기본 구문
```python
try:
    실행할 코드
except:
    예외가 발생했을 때 처리하는 코드
else:
    예외가 발생하지 않았을 때 실행할 코드
finally:
    예외 발생 여부와 상관없이 항상 실행할 코드
```

```python
try:
    x = int(input('나눌 숫자를 입력하세요: '))
    y = 10 / x
except ZeroDivisionError:    # 숫자를 0으로 나눠서 에러가 발생했을 때 실행됨
    print('숫자를 0으로 나눌 수 없습니다.')
else:                        # try의 코드에서 예외가 발생하지 않았을 때 실행됨
    print(y)
finally:                     # 예외 발생 여부와 상관없이 항상 실행됨
    print('코드 실행이 끝났습니다.')

```
{: .note}
> try 안에서 만든 변수는 try 바깥에서 사용할 수 있나요?
try는 함수가 아니므로 스택 프레임을 만들지 않습니다 따라서 try 안에서 변수를 만들더라도 try 바깥에서 사용할 수 있습니다. 물론 except, else, finally에서도 사용할 수 있습니다.

- 에러 메시지는 변수다.

In some languages, errors are indicated by special function return values. When things go south, Python uses exceptions: code that is executed when an associated error occurs.

You’ve seen some of these already, such as accessing a list or tuple with an out-of-range position, or a dictionary with a nonexistent key. When you run code that might fail under some circumstances, you also need appropriate exception handlers to intercept any potential errors.

It’s good practice to add exception handling anywhere an exception might occur to let the user know what is happening. You might not be able to fix the problem, but at least you can note the circumstances and shut your program down gracefully. If an exception occurs in some function and is not caught there, it bubbles up until it is caught by a matching handler in some calling function. If you don’t provide your own exception handler, Python prints an error message and some information about where the error occurred and then terminates the program, as demonstrated in the following snippet:

```python
short_list = [1, 2, 3]
position = 5
print(short_list[position])
'''
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
IndexError: list index out of range
'''
```
#### Handle Errors with try and except

Rather than leaving things to chance, use try to wrap your code, and except to provide the error handling:

```python
short_list = [1, 2, 3]
position = 5
try :
    short_list[position]
except :
    print ('Need a position between 0 and', len(short_list)-1, ' but got', position)
'''
Need a position between 0 and 2 but got 5
'''
```
The code inside the try block is run. If there is an error, an exception is raised and the code inside the except block runs. If there are no errors, the except block is skipped.

Specifying a plain except with no arguments, as we did here, is a catchall for any exception type. If more than one type of exception could occur, it’s best to provide a separate exception handler for each. No one forces you to do this; you can use a bare except to catch all exceptions, but your treatment of them would probably be generic (something akin to printing Some error occurred). You can use any number of specific exception handlers.

Sometimes, you want exception details beyond the type. You get the full exception object in the variable name if you use the form:

```python
except exceptiontype as name
```
The example that follows looks for an IndexError first, because that’s the exception type raised when you provide an illegal position to a sequence. It saves an IndexError exception in the variable err, and any other exception in the variable other. The example prints everything stored in other to show what you get in that object:


```python
short_list = [1, 2, 3]
while True:
    value = input('Position [q to quit]? ')
    if value == 'q':
        break
    try :
        position = int(value)
        print (short_list[position])
    except IndexError as err:
        print ('Bad index:', position)
    except Exception as other:
        print ('Something else broke:', other)
```
```python
Position [q to quit]? 1
2
Position [q to quit]? 0
1
Position [q to quit]? 2
3
Position [q to quit]? 3
Bad index: 3
Position [q to quit]? 2
3
Position [q to quit]? two
Something else broke: invalid literal for int() with base 10: 'two'
Position [q to quit]? q
```
Inputting position 3 raised an IndexError as expected. Entering two annoyed the int() function, which we handled in our second, catchall except code.

#### Make Your Own Exceptions

The previous section discussed handling exceptions, but all of the exceptions (such as IndexError) were predefined in Python or its standard library. You can use any of these for your own purposes. You can also define your own exception types to handle special situations that might arise in your own programs.

{: .note}
> This requires defining a new object type with a class — something we don’t get into until Chapter 10. So, if you’re unfamiliar with classes, you might want to return to this section later.

An exception is a class. It is a child of the class Exception. Let’s make an exception called UppercaseException and raise it when we encounter an uppercase word in a string:

```python
class UppercaseException ( Exception ):
    pass

words = ['eenie', 'meenie', 'miny', 'MO']
for word in words:
    if word.isupper():
        raise UppercaseException(word)
'''
Traceback (most recent call last):
File "<stdin>", line 3, in <module>
__main__.UppercaseException: MO
'''
```

We didn’t even define any behavior for UppercaseException (notice we just used pass), letting its parent class Exception figure out what to print when the exception was raised.

You can access the exception object itself and print it:

```python
try :
    raise OopsException('panic')
except OopsException as exc:
    print (exc)
    
'''
panic
'''
```
- 클래스 생성 시 에러메시지 초기화 방법

```python
class 예외이름(Exception):
    def __init__(self):
        super().__init__('에러메시지')
```

```python
class NotThreeMultipleError(Exception):    # Exception을 상속받아서 새로운 예외를 만듦
    def __init__(self):
        super().__init__('3의 배수가 아닙니다.')
 
def three_multiple():
    try:
        x = int(input('3의 배수를 입력하세요: '))
        if x % 3 != 0:                     # x가 3의 배수가 아니면
            raise NotThreeMultipleError    # NotThreeMultipleError 예외를 발생시킴
        print(x)
    except Exception as e:
        print('예외가 발생했습니다.', e)
 
three_multiple()

'''
3의 배수를 입력하세요: 5 (입력)
예외가 발생했습니다. 3의 배수가 아닙니다.
'''
```

#### 예외 발생 시키기

- raise Exception('에러메시지')
```python
try:
    x = int(input('3의 배수를 입력하세요: '))
    if x % 3 != 0:                                 # x가 3의 배수가 아니면
        raise Exception('3의 배수가 아닙니다.')    # 예외를 발생시킴
    print(x)
except Exception as e:                             # 예외가 발생했을 때 실행됨
    print('예외가 발생했습니다.', e)

'''
3의 배수를 입력하세요: 5 (입력)
예외가 발생했습니다. 3의 배수가 아닙니다.
'''
```
- 예외처리 메커니즘   
예외가 발생하더라도 현재 코드 블록에서 처리해줄 except가 없다면 except가 나올 때까지 계속 상위 코드 블록으로 올라갑니다.   
만약 함수 바깥에도 처리해줄 except가 없다면 코드 실행은 중지되고 에러가 표시됩니다.    

- 현재 예외를 다시 발생시키기
이번에는 try except에서 처리한 예외를 다시 발생시키는 방법입니다.    
except 안에서 raise를 사용하면 현재 예외를 다시 발생시킵니다(re-raise).

```python
def three_multiple():
    try:
        x = int(input('3의 배수를 입력하세요: '))
        if x % 3 != 0:                                 
            raise Exception('3의 배수가 아닙니다.')    
        print(x)
    except Exception as e:                             
        print('three_multiple 함수에서 예외가 발생했습니다.', e)
        raise    # raise로 현재 예외를 다시 발생시켜서 상위 코드 블록으로 넘김
 
try:
    three_multiple()
except Exception as e:                                 # 하위 코드 블록에서 예외가 발생해도 실행됨
    print('스크립트 파일에서 예외가 발생했습니다.', e)
```

#### assert로 예외 발생시키기

예외를 발생시키는 방법 중에는 assert를 사용하는 방법도 있습니다.    
assert는 지정된 조건식이 거짓일 때 AssertionError 예외를 발생시킨다.    
assert는 디버깅 모드에서만 실행됩니다. 
    : 파이썬은 기본적으로 디버깅 모드(`__debug__` 값이 True)  / 
        assert가 실행되지 않게 하려면 -O 옵션을 붙여서 실행합니다(영문 대문자 O): python -O 스크립트파일.py

- assert 조건식
- assert 조건식, 에러메시지

```python
x = int(input('3의 배수를 입력하세요: '))
assert x % 3 == 0, '3의 배수가 아닙니다.'    # 3의 배수가 아니면 예외 발생, 3의 배수이면 그냥 넘어감
print(x)

'''
3의 배수를 입력하세요: 5 (입력)

Traceback (most recent call last):
  File "C:\project\assertion.py", line 2, in <module>
    assert x % 3 == 0, '3의 배수가 아닙니다.'
AssertionError: 3의 배수가 아닙니다.
'''
```




### Coming Up

Objects! We had to get to them sometime in a book about an object-oriented language.

### Things to Do

9.1 Define a function called good() that returns the following list: ['Harry', 'Ron', 'Hermione'].   
```
def good():
    return ['Harry', 'Ron', 'Hermione']
```
9.2 Define a generator function called get_odds() that returns the odd numbers from range(10). Use a for loop to find and print the third value returned.    
```
def get_odds():
    for i in range(10):
        if i%2 != 0:
            yield i
n=0            
for i in get_odds():
    if n<3:
        print(i)
    n+=1
```
9.3 Define a decorator called test that prints 'start' when a function is called, and 'end' when it finishes.  
```
def test(func):
    def new_func(*args, **kwargs):
        print ('start')
        result = func(*args, **kwargs)
        print ('end')
        return result
    return new_func

@test
def greeting():
    print ("Greetings, Earthling")

greeting()
``` 
9.4 Define an exception called OopsException. Raise this exception to see what happens. Then, write the code to catch this exception and print 'Caught an oops'.
```
class OopsException(Exception):
    pass

try:
    raise OopsException
except OopsException :
    print("Caught an oops")
```

## 일급 객체란 무엇인가요?

일급 객체(first-class object)란 다음 조건을 만족하는 객체를 뜻합니다.

- 변수나 데이터 구조에 넣을 수 있어야 한다.
- 매개변수에 전달할 수 있어야 한다.
- 반환값으로 사용할 수 있어야 한다.

특히 일급 함수(first-class function)는 일급 객체의 조건을 만족하면서 실행 중(run-time)에 함수를 생성할 수 있어야 합니다. 파이썬에서는 def 안에서 def로 함수를 만들거나, lambda를 사용하여 실행 중에 함수를 생성할 수 있으므로 파이썬의 함수는 일급 함수입니다.

## 다른 언어에 있는 switch 문법은 사용할 수 없나요?

파이썬은 switch 문법이 없습니다. 하지만 딕셔너리와 람다 표현식을 사용하면 switch처럼 사용할 수는 있습니다.
```python
switch = {
    '+': lambda x, y: x + y,    # 람다 표현식으로 실행할 코드를 작성
    '*': lambda x, y: x * y
    }
 
x = '+'
try:
    print(switch[x](10, 20))    # 딕셔너리에 키를 지정하는 방식
except KeyError:
    print('default')            # 딕셔너리에 키가 없을 때는 기본값
```