---
layout: default
title: turtle
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

[docs.python.org](https://docs.python.org/ko/3/library/turtle.html)

```python
from turtle import *
tt = Turtle()          # 그리기 객체 생성
tt.speed(0)
tt.color('blue')
tt.shape('turtle')     # 거북이 모양
for i in range(0,250,5):
    tt.fd(i)
    tt.rt(90)
# 화면 자동 닫힘 방지 - 코드 마지막에 위치 해야 함
mainloop()
``` 

## Exercise 1

```python
from turtle import *
import math

def square(t, length):
    for i in range(4):
        t.fd(length)
        t.lt(90)


def polyline(t, n, length, angle):
    """
    t: Turtle object
    n: number of line segments
    length: length of each segment
    angle: degrees between segments
    """
    for i in range(n):
        t.fd(length)
        t.lt(angle)


def polygon(t, n, length):
    """
    t: Turtle
    n: number of sides
    length: length of each side.
    """
    angle = 360.0/n
    polyline(t, n, length, angle)


def arc(t, r, angle):
    """
    t: Turtle
    r: radius
    angle: angle subtended by the arc, in degrees
    """
    arc_length = 2 * math.pi * r * abs(angle) / 360
    n = int(arc_length / 4) + 3
    step_length = arc_length / n
    step_angle = float(angle) / n

    # making a slight left turn before starting reduces
    # the error caused by the linear approximation of the arc
    t.lt(step_angle/2)
    polyline(t, n, step_length, step_angle)
    t.rt(step_angle/2)


def circle(t, r):
    """
    t: Turtle
    r: radius
    """
    arc(t, r, 360)


# the following condition checks whether we are
# running as a script, in which case run the test code,
# or being imported, in which case don't.

if __name__ == '__main__':

    bob = Turtle()  # 그리기 객체 생성
    bob.speed(0)
    bob.color('blue')

    square(bob, 200)
    polyline(bob, 6, 10, 60)
    polygon(bob, 6, 100)

    # draw a circle centered on the origin
    radius = 100
    bob.pu()
    bob.fd(radius)
    bob.lt(90)
    bob.pd()
    circle(bob, radius)

    # 화면 자동 닫힘 방지 - 코드 마지막에 위치 해야 함
    mainloop()
``` 

## Exercise 2

```python
import turtle

from polygon import arc


def petal(t, r, angle):
    """Draws a petal using two arcs.

    t: Turtle
    r: radius of the arcs
    angle: angle (degrees) that subtends the arcs
    """
    for i in range(2):
        arc(t, r, angle)
        t.lt(180-angle)


def flower(t, n, r, angle):
    """Draws a flower with n petals.

    t: Turtle
    n: number of petals
    r: radius of the arcs
    angle: angle (degrees) that subtends the arcs
    """
    for i in range(n):
        petal(t, r, angle)
        t.lt(360.0/n)


def move(t, length):
    """Move Turtle (t) forward (length) units without leaving a trail.
    Leaves the pen down.
    """
    t.pu()
    t.fd(length)
    t.pd()


bob = turtle.Turtle()
bob.speed(0)
bob.color('blue')
bob.shape('turtle')     # 거북이 모양

# draw a sequence of three flowers, as shown in the book.
move(bob, -100)
flower(bob, 7, 60.0, 60.0)

move(bob, 100)
flower(bob, 10, 40.0, 80.0)

move(bob, 100)
flower(bob, 20, 140.0, 20.0)

bob.hideturtle()
turtle.mainloop()
``` 

## Exercise 3

```python
import math
import turtle


def draw_pie(t, n, r):
    """Draws a pie, then moves into position to the right.

    t: Turtle
    n: number of segments
    r: length of the radial spokes
    """
    polypie(t, n, r)
    t.pu()
    t.fd(r*2 + 10)
    t.pd()


def polypie(t, n, r):
    """Draws a pie divided into radial segments.

    t: Turtle
    n: number of segments
    r: length of the radial spokes
    """
    angle = 360.0 / n
    for i in range(n):
        isosceles(t, r, angle/2)
        t.lt(angle)


def isosceles(t, r, angle):
    """Draws an icosceles triangle.

    The turtle starts and ends at the peak, facing the middle of the base.

    t: Turtle
    r: length of the equal legs
    angle: half peak angle in degrees
    """
    y = r * math.sin(angle * math.pi / 180)

    t.rt(angle)
    t.fd(r)
    t.lt(90+angle)
    t.fd(2*y)
    t.lt(90+angle)
    t.fd(r)
    t.lt(180-angle)


bob = turtle.Turtle()
bob.speed(0)
bob.color('blue')
bob.shape('turtle')     # 거북이 모양

bob.pu()
bob.bk(130)
bob.pd()

# draw polypies with various number of sides
size = 40
draw_pie(bob, 5, size)
draw_pie(bob, 6, size)
draw_pie(bob, 7, size)
draw_pie(bob, 8, size)

bob.hideturtle()
turtle.mainloop()
```

## Exercise 4

![Alt text](/assets/images/%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C100.png)

```python
"""This module contains a code example related to

Think Python, 2nd Edition
by Allen Downey
http://thinkpython2.com

Copyright 2015 Allen Downey

License: http://creativecommons.org/licenses/by/4.0/
"""

from __future__ import print_function, division

import turtle

from polygon import circle, arc

# LEVEL 0 PRIMITIVES 
# fd, bk, lt, rt, pu, pd

def fd(t, length):
    t.fd(length)

def bk(t, length):
    t.bk(length)

def lt(t, angle=90):
    t.lt(angle)

def rt(t, angle=90):
    t.rt(angle)

def pd(t):
    t.pd()

def pu(t):
    t.pu()


# LEVEL 1 PRIMITIVES are simple combinations of Level 0 primitives.
# They have no pre- or post-conditions.

def fdlt(t, n, angle=90):
    """forward and left"""
    fd(t, n)
    lt(t, angle)

def fdbk(t, n):
    """forward and back, ending at the original position"""
    fd(t, n)
    bk(t, n)

def skip(t, n):
    """lift the pen and move"""
    pu(t)
    fd(t, n)
    pd(t)

def stump(t, n, angle=90):
    """Makes a vertical line and leave the turtle at the top, facing right"""
    lt(t)
    fd(t, n)
    rt(t, angle)

def hollow(t, n):
    """move the turtle vertically and leave it at the top, facing right"""
    lt(t)
    skip(t, n)
    rt(t)


# LEVEL 2 PRIMITIVES use primitives from Levels 0 and 1
# to draw posts (vertical elements) and beams (horizontal elements)
# Level 2 primitives ALWAYS return the turtle to the original
# location and direction.

def post(t, n):
    """Makes a vertical line and return to the original position"""
    lt(t)
    fdbk(t, n)
    rt(t)

def beam(t, n, height):
    """Makes a horizontal line at the given height and return."""
    hollow(t, n*height)
    fdbk(t, n)
    hollow(t, -n*height)

def hangman(t, n, height):
    """Makes a vertical line to the given height and a horizontal line
    at the given height and then return.
    This is efficient to implement, and turns out to be useful, but
    it's not so semantically clean."""
    stump(t, n * height)
    fdbk(t, n)
    lt(t)
    bk(t, n*height)
    rt(t)

def diagonal(t, x, y):
    """Makes a diagonal line to the given x, y offsets and return"""
    from math import atan2, sqrt, pi
    angle = atan2(y, x) * 180 / pi
    dist = sqrt(x**2 + y**2)
    lt(t, angle)
    fdbk(t, dist)
    rt(t, angle)

def vshape(t, n, height):
    diagonal(t, -n/2, height*n)
    diagonal(t, n/2, height*n)

def bump(t, n, height):
    """Makes a bump with radius n at height*n 
    """
    stump(t, n*height)
    arc(t, n/2.0, 180)
    lt(t)
    fdlt(t, n*height+n)


"""
The letter-drawing functions all have the precondition
that the turtle is in the lower-left corner of the letter,
and postcondition that the turtle is in the lower-right
corner, facing in the direction it started in.

They all take a turtle as the first argument and a size (n)
as the second.  Most letters are (n) units wide and (2n) units
high.

"""

def draw_a(t, n):
    diagonal(t, n/2, 2*n)
    beam(t, n, 1)
    skip(t, n)
    diagonal(t, -n/2, 2*n)

def draw_b(t, n):
    bump(t, n, 1)
    bump(t, n, 0)
    skip(t, n/2)

def draw_c(t, n):
    hangman(t, n, 2)
    fd(t, n)

def draw_d(t, n):
    bump(t, 2*n, 0)
    skip(t, n)

def draw_ef(t, n):
    hangman(t, n, 2)
    hangman(t, n, 1)

def draw_e(t, n):
    draw_ef(t, n)
    fd(t, n)

def draw_f(t, n):
    draw_ef(t, n)
    skip(t, n)

def draw_g(t, n):
    hangman(t, n, 2)
    fd(t, n/2)
    beam(t, n/2, 2)
    fd(t, n/2)
    post(t, n)

def draw_h(t, n):
    post(t, 2*n)
    hangman(t, n, 1)
    skip(t, n)
    post(t, 2*n)

def draw_i(t, n):
    beam(t, n, 2)
    fd(t, n/2)
    post(t, 2*n)
    fd(t, n/2)

def draw_j(t, n):
    beam(t, n, 2)
    arc(t, n/2, 90)
    fd(t, 3*n/2)
    skip(t, -2*n)
    rt(t)
    skip(t, n/2)

def draw_k(t, n):
    post(t, 2*n)
    stump(t, n, 180)
    vshape(t, 2*n, 0.5)
    fdlt(t, n)
    skip(t, n)

def draw_l(t, n):
    post(t, 2*n)
    fd(t, n)

def draw_n(t, n):
    post(t, 2*n)
    skip(t, n)
    diagonal(t, -n, 2*n)
    post(t, 2*n)

def draw_m(t, n):
    post(t, 2*n)
    draw_v(t, n)
    post(t, 2*n)

def draw_o(t, n):
    skip(t, n)
    circle(t, n)
    skip(t, n)

def draw_p(t, n):
    bump(t, n, 1)
    skip(t, n/2)

def draw_q(t, n):
    draw_o(t, n)
    diagonal(t, -n/2, n)

def draw_r(t, n):
    draw_p(t, n)
    diagonal(t, -n/2, n)

def draw_s(t, n):
    fd(t, n/2)
    arc(t, n/2, 180)
    arc(t, n/2, -180)
    fdlt(t, n/2, -90)
    skip(t, 2*n)
    lt(t)

def draw_t(t, n):
    beam(t, n, 2)
    skip(t, n/2)
    post(t, 2*n)
    skip(t, n/2)

def draw_u(t, n):
    post(t, 2*n)
    fd(t, n)
    post(t, 2*n)

def draw_v(t, n):
    skip(t, n/2)
    vshape(t, n, 2)
    skip(t, n/2)

def draw_w(t, n):
    draw_v(t, n)
    draw_v(t, n)

def draw_x(t, n):
    diagonal(t, n, 2*n)
    skip(t, n)
    diagonal(t, -n, 2*n)

def draw_v(t, n):
    skip(t, n/2)
    diagonal(t, -n/2, 2*n)
    diagonal(t, n/2, 2*n)
    skip(t, n/2)

def draw_y(t, n):
    skip(t, n/2)
    stump(t, n)
    vshape(t, n, 1)
    rt(t)
    fdlt(t, n)
    skip(t, n/2)

def draw_z(t, n):
    beam(t, n, 2)
    diagonal(t, n, 2*n)
    fd(t, n)

def draw_(t, n):
    # draw a space
    skip(t, n)

if __name__ == '__main__':

    # create and position the turtle
    size = 20
    bob = turtle.Turtle()

    for f in [draw_h, draw_e, draw_l, draw_l, draw_o]:
        f(bob, size)
        skip(bob, size)

    turtle.mainloop()

```

```python
"""This module contains a code example related to

Think Python, 2nd Edition
by Allen Downey
http://thinkpython2.com

Copyright 2015 Allen Downey

License: http://creativecommons.org/licenses/by/4.0/
"""

from __future__ import print_function, division

import math
import turtle


def square(t, length):
    """Draws a square with sides of the given length.

    Returns the Turtle to the starting position and location.
    """
    for i in range(4):
        t.fd(length)
        t.lt(90)


def polyline(t, n, length, angle):
    """Draws n line segments.

    t: Turtle object
    n: number of line segments
    length: length of each segment
    angle: degrees between segments
    """
    for i in range(n):
        t.fd(length)
        t.lt(angle)


def polygon(t, n, length):
    """Draws a polygon with n sides.

    t: Turtle
    n: number of sides
    length: length of each side.
    """
    angle = 360.0/n
    polyline(t, n, length, angle)


def arc(t, r, angle):
    """Draws an arc with the given radius and angle.

    t: Turtle
    r: radius
    angle: angle subtended by the arc, in degrees
    """
    arc_length = 2 * math.pi * r * abs(angle) / 360
    n = int(arc_length / 4) + 3
    step_length = arc_length / n
    step_angle = float(angle) / n

    # making a slight left turn before starting reduces
    # the error caused by the linear approximation of the arc
    t.lt(step_angle/2)
    polyline(t, n, step_length, step_angle)
    t.rt(step_angle/2)


def circle(t, r):
    """Draws a circle with the given radius.

    t: Turtle
    r: radius
    """
    arc(t, r, 360)


# the following condition checks whether we are
# running as a script, in which case run the test code,
# or being imported, in which case don't.

if __name__ == '__main__':
    bob = turtle.Turtle()

    # draw a circle centered on the origin
    radius = 100
    bob.pu()
    bob.fd(radius)
    bob.lt(90)
    bob.pd()
    circle(bob, radius)

    # wait for the user to close the window
    turtle.mainloop()

```
  
```python
"""This module contains a code example related to

Think Python, 2nd Edition
by Allen Downey
http://thinkpython2.com

Copyright 2015 Allen Downey

License: http://creativecommons.org/licenses/by/4.0/
"""

from __future__ import print_function, division

import string
import turtle

"""
To use this typewriter, you have to provide a module named letters.py
that contains functions with names like draw_a, draw_b, etc.
"""

# check if the reader has provided letters.py
try:
    import letters
except ImportError as e:
    message = e.args[0]
    if message.startswith('No module'):
        raise ImportError(message + 
                          '\nYou have to provide a module named letters.py')


def teleport(t, x, y):
    """Moves the turtle without drawing a line.

    Postcondition: pen is down

    t: Turtle
    x: coordinate
    y: coordinate
    """
    t.pu()
    t.goto(x, y)
    t.pd()


def keypress(char):
    """Handles the event when a user presses a key.

    Checks if there is a function with the right name; otherwise
    it prints an error message.

    char: string, letter to draw
    """
    # if we're still drawing the previous letter, bail out
    if bob.busy:
        return
    else:
        bob.busy = True

    # figure out which function to call, and call it
    try:
        name = 'draw_' + char
        func = getattr(letters, name)
    except AttributeError:
        print("I don't know how to draw an", char)
        bob.busy = False
        return

    func(bob, size)

    letters.skip(bob, size/2)
    bob.busy = False


def carriage_return():
    """Moves to the beginning of the next line.
    """
    teleport(bob, -180, bob.ycor() - size*3)
    bob.busy = False


def presser(char):
    """Returns a function object that executes keypress.

    char: character to draw when the function is executed

    returns: function with no arguments
    """
    def func():
        keypress(char)
    return func


# create and position the turtle
size = 20
bob = turtle.Turtle()
bob.busy = False
teleport(bob, -180, 150)

# tell world to call keypress when the user presses a key
screen = bob.getscreen()

for char in string.ascii_lowercase:
    screen.onkey(presser(char), char)

screen.onkey(carriage_return, 'Return')

screen.listen()
turtle.mainloop()

```
 
## Exercise 5

![Alt text](/assets/images/%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C101.png)

```python
"""This module contains a code example related to

Think Python, 2nd Edition
by Allen Downey
http://thinkpython2.com

Copyright 2015 Allen Downey

License: http://creativecommons.org/licenses/by/4.0/
"""

from __future__ import print_function, division

import turtle


def draw_spiral(t, n, length=3, a=0.1, b=0.0002):
    """Draws an Archimedian spiral starting at the origin.

    Args:
      n: how many line segments to draw
      length: how long each segment is
      a: how loose the initial spiral starts out (larger is looser)
      b: how loosly coiled the spiral is (larger is looser)

    http://en.wikipedia.org/wiki/Spiral
    """
    theta = 0.0

    for i in range(n):
        t.fd(length)
        dtheta = 1 / (a + b * theta)

        t.lt(dtheta)
        theta += dtheta


# create the world and bob
bob = turtle.Turtle()
draw_spiral(bob, n=1000)

turtle.mainloop()

```
 

## Exercise 6
```python
"""This module contains a code example related to

Think Python, 2nd Edition
by Allen Downey
http://thinkpython2.com

Copyright 2015 Allen Downey

License: http://creativecommons.org/licenses/by/4.0/
"""

from __future__ import print_function, division

import turtle


def koch(t, n):
    """Draws a koch curve with length n."""
    if n < 10:
        t.fd(n)
        return
    m = n/3
    koch(t, m)
    t.lt(60)
    koch(t, m)
    t.rt(120)
    koch(t, m)
    t.lt(60)
    koch(t, m)


def snowflake(t, n):
    """Draws a snowflake (a triangle with a Koch curve for each side)."""
    for i in range(3):
        koch(t, n)
        t.rt(120)


bob = turtle.Turtle()

bob.pu()
bob.goto(-150, 90)
bob.pd()
snowflake(bob, 300)

turtle.mainloop()
```

## Exercise 7
```python
from turtle import *
color('red', 'yellow')
begin_fill()
while True:
    forward(200)
    left(170)
    if abs(pos()) < 1:
        break
end_fill()
done()
``` 


## Exercise 8
```python
import turtle as t

def star(number:int=5,length:int = 150) -> None:
    t.shape('turtle')
    t.speed('fastest')

    angle = (-360/number + 90)
    for i in range(number):    
        t.fd(length)
        t.rt(180-2*angle)
        t.fd(length)
        t.lt(90-angle)
    t.mainloop()
    
    
star(6,150)
``` 