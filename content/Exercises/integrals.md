---
title: "Numeric Integration"
date: 2018-06-20T14:43:15-04:00
draft: draft
weight: 1500
---

Objectives
----------

- Practice writing Python functions.
- Gain experience with list comprehensions.
- Write helper functions and compose large functions from smaller ones.

Background
----------

In this lab you will build a `python` program that can compute the areas underneath arbitrary mathematical functions (mathematicians call these *integrals*). In addition, you'll calculate answers that mathematicians don't have formulas for...and you'll never have to use anything more complicated than multiplication! 

**Getting started...**

Start by creating a new file, we will call ours `integrals.py`, and pasting this code into it:

~~~text
# Vassar CS Camp 
# Name: [your name here]
# Filename: integrals.py

# this gives us functions like sin and cos...
from math import *

# two more functions (not in the math library above)

def dbl(x):
    """Doubler!  argument: x, a number"""
    return 2*x

def sq(x):
    """Squarer!  argument: x, a number"""
    return x**2

# examples for getting used to list comprehensions...

def lc_mult(N):
    """This example accepts an integer N
       and returns a list of integers
       from 0 to N-1, **each multiplied by 2**
    """
    return [2*x for x in range(N)]

def lc_idiv(N):
    """This example accepts an integer N
       and returns a list of integers
       from 0 to N-1, **each divided by 2**
       WARNING: this is INTEGER division...!
    """
    return [x//2 for x in range(N)]

def lc_fdiv(N):
    """This example accepts an integer N
       and returns a list of integers
       from 0 to N-1, **each divided by 2**
       NOTE: this is floating-point division...!
    """
    return [x/2 for x in range(N)]

assert lc_mult(4) == [0, 2, 4, 6]
assert lc_idiv(4) == [0, 0, 1, 1]
assert lc_fdiv(4) == [0.0, 0.5, 1.0, 1.5]

# Here is where your functions start for the exercise:

# Step 1, part 1
def unitfracs(N):
    """Be sure to improve this docstring!
    """
    pass  # replace this line (pass is Python's empty statement)
~~~

**Trying out *list comprehensions***

To begin, try out list comprehensions at the Python prompt... these examples should help build intuition about how list comprehensions work:
~~~text
>>> lc_mult(10)   # multiplication example
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
>>> lc_mult(5)    # a smaller example
[0, 2, 4, 6, 8]
>>> lc_idiv(10)   # integer division
[0, 0, 1, 1, 2, 2, 3, 3, 4, 4]
>>> lc_fdiv(10)   # floating-point division
[0.0, 0.5, 1.0, 1.5, 2.0, 2.5, 3.0, 3.5, 4.0, 4.5]
~~~

Read over those three one-line functions; be sure you have internalized how they work!

Note that the calls `lc_idiv(10)` and `lc_fdiv(10)` return different lists; the first uses integer division (rounding down); the second uses floating-point division.

Integration: why? and what?
---------------------------
Integration is sometimes described as finding the area between a mathematical function and the horizontal (x) axis.

More generally, integration is simply the sum of a numeric function's results, i.e., y-values across a chosen span.

It is important because it provides a one-number summary of what the function is "doing" over an interval. It's also used to determine how fields of forces act on a particular point, surface, or object over time; it is also essential in defining a function's "average value" on an interval or region. Integrals can be used to design an airplane wing, predict the weather, or calculate how much a bank account will be worth in ten years even if interest rates are changing.

As an example, recall the `dbl` function from above (with a better docstring):

~~~text
def dbl(x):
    """Argument: a number x (int or float)
       Return value: twice the argument
    """
    return 2*x
~~~
This function could be written algebraically as `y = 2x`, where `y` is the functions return value and `x` is its input.

Suppose you wanted to estimate the integral of `dbl`, on the interval between 0.0 and 10.0. You could create the following (rough) approximation with rectangles: 

![y=2x](/images/integrals/y2x.png)


1. Here, the interval is divided into 4 parts. The list `[0, 2.5, 5, 7.5]` contains each `x` value of the *left-hand endpoint of each of the four subintervals*.
2. We next find the return values from `dbl(x)` for each possible `x` in the list above. Here, we name these return values `y`. The list of these values is `[0, 5, 10, 15]`.
3. Now we add up the areas of the rectangles whose upper-left-hand corner (height) is at these `y` values. Each rectangle extends down to the `x`-axis. Each rectangle's individual width is 2.5, because there are four equal-width rectangles spanning a total of 10 units of width.
4. We find the rectangles' areas in the usual way. Their heights are contained in the list `y` and their widths are 2.5, so the total area is
`0*2.5 + 5*2.5 + 10*2.5 + 15*2.5`
or
`(0 + 5 + 10 + 15)*2.5`
which is `(30)*2.5`, or `75`.

Yes, this is a very rough approximation for the "area under the curve," i.e., the integral. But if we make the width of the rectangles smaller, their sum will approximate that area as closely as we'd like!

More importantly, this example suggests a general way to approximate a function's integral over a known interval:

1. Divide the interval into `N` equal parts and create a list with the corresponding `x` (argument) values.
2. Find the `y` values (results) of the function for each value of `x` calculated in step 1
3. Calculate the area of each rectangle under the curve. Their heights are the `y` values; their widths are the separation between the `x` values.
4. Sum the rectangles' areas and return the result: that's the integral, or an approximation that can be made arbitrarily close by adding more rectangles. 

The rest of this exercise involves writing functions for each of these four steps; then you'll use those functions to answer questions about the results. 

Step 1: Calculating the x values to be evaluated
------------------------------------------------

First, you will write a function named `unitfracs(N)` and then one named `scaledfracs(low, hi, N)`. 

**Writing `unitfracs`...**
Writing unitfracs ...

Take a look at how `unitfracs(N)` works:
~~~text
>>> unitfracs(2)
[0.0, 0.5]
>>> unitfracs(4)
[0.0, 0.25, 0.5, 0.75]
>>> unitfracs(5)
[0.0, 0.2, 0.4, 0.6, 0.8]
>>> unitfracs(3)
[0.0, 0.3333333333333333, 0.6666666666666666]
>>> unitfracs(10)
[0.0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9]
~~~

> **To do**: Write `unitfracs(N)`.
> 
> As its name suggests, it returns a list of evenly-spaced left-hand endpoints (fractions) in the unit interval [0, 1).
>
{{% notice tip %}}
Copy, paste, and alter the example function `lc_fdiv` in order to write `unitfracs`. You will only need to change a single character from that code!
{{% /notice %}}
> 
> Be sure to write the docstring of `unitfracs` to reflect what it does, as well.
> 
> And finally, write at least three `assert` statements that implement tests for some of the examples above. 

**Writing `scaledfracs`...**

Next, take a look at how `scaledfracs(low, hi, N)` works:
~~~text
>>> scaledfracs(10, 30, 5)
[10.0, 14.0, 18.0, 22.0, 26.0]
>>> scaledfracs(41, 43, 8)
[41.0, 41.25, 41.5, 41.75, 42.0, 42.25, 42.5, 42.75]
>>> scaledfracs(0, 10, 4)
[0.0, 2.5, 5.0, 7.5]
~~~

> **To do**: Write `scaledfracs(low, hi, N)`. It creates `N` left endpoints uniformly through the interval [low, hi).
> 
> Again, write assert statements to test the examples above.
> 
{{% notice tip %}}
This is tricky ... here is some additional explanation:
<br>
Use `unitfracs`. For example, use this line as a starting point:
<br>
`return [                      for x in unitfracs(N)]`
<br>
This way, you won't have to redo the work of `unitfracs`!
{{% /notice %}}
> You might feel that this is closely related to the interp function you wrote before---you're right!
> 
> You don't need to use that interp function, but you will want to use the ideas from it! Here it is, for reference:
> 
~~~text
def interp(low, hi, frac):
    """Returns a value frac of the way from low to hi"""
    return low + (hi-low)*frac
~~~
> Note that the role of `frac` above is as the "interpolating fraction," which is exactly what `x` is doing in the list comprehension!
> 
> Do include a docstring that reflects what `scaledfracs` does. 

Step 2: Calculating the `y` values
--------------------------------

Your `scaledfracs` function can produce arbitrary lists of evenly-spaced `x` values.

Next, you'll need to calculate the `y` values (results) of a function at each of these `x` positions. Again, you'll use list comprehensions to make this process simple and fast!

Although the goal is to handle arbitrary functions, we'll start with a concrete function and build up. 

**Writing `sqfracs`...**
 
> **To do**: Write a function `sqfracs(low, hi, N)` that works as follows:
~~~text
>>> sqfracs(4, 10, 6)
[16.0, 25.0, 36.0, 49.0, 64.0, 81.0]
>>> sqfracs(0, 10, 5)
[0.0, 4.0, 16.0, 36.0, 64.0]
~~~
>
> Here, `sqfracs` is very similar to `scaledfracs` except that each value is squared.
> 
{{% notice tip %}}
Use `scaledfracs` here. In the same way that `scaledfracs` used `unitfracs`, `sqfracs` can use `scaledfracs`! Consider the snippet:
<br>
`for x in scaledfracs(low, hi, N)`
{{{% /notice %}}
As usual, write some `assert`s to test `sqfracs`. For extra fun, concoct some additional examples of your own!

**Writing `f_of_fracs`...**

> **To do**: Write a function `f_of_fracs(f, low, hi, N)` that works as follows:
~~~text
>>> f_of_fracs(dbl, 10, 20, 5)
[20.0, 24.0, 28.0, 32.0, 36.0]
>>> f_of_fracs(sq, 4, 10, 6)
[16.0, 25.0, 36.0, 49.0, 64.0, 81.0]
>>> f_of_fracs(sin, 0, pi, 4)   # the sine function
[0.0, 0.71, 1.0, 0.71]
# the above values are rounded versions of what 
# will actually be displayed...
~~~
> 
> Note that `f_of_fracs` takes a *function* as its first argument---this is no problem in `python`.
>
> You might copy and paste `sqfracs` as a model: only a few characters need to be changed! (You only need 3 keystrokes to fix this one!)
> 
> The third example above is tricky to test with assert---it can be done, but it's hard to do properly. Note that it's not correct to run `f_of_fracs(sin, ...)` and then copy its output into an `assert` statement: in that case you would be saying "the right answer is the one my function calculated, even if my function got the wrong answer!"

Step 3: Calculate the area and put it all together
--------------------------------------------------

You now have functions that calculate both the `x` and, more importantly, the `y` values of a function at regularly-spaced intervals. Well done! Now we just have to put it all together.

> **To do**: Write `integrate(f, low, hi, N)` which will return the final, desired value: the integral of `f` from `low` to `hi` using `N` steps.
> 
> Take a look at a few examples and hints below.
> 
> As these examples highlight, `integrate` does not return a list; it returns a single, floating-point value:
~~~text
>>> import math                  # to use math.pi and math.sin
>>> integrate(dbl, 0, 10, 4)
75.0                         # the example from the top of this lab
>>> integrate(dbl, 0, 10, 1000)
99.9                         # rounded from 99.8999... (precise value: 100)
>>> integrate(sq, 0, 3, 1000000) # a million steps will give Python pause
8.9999865000044963           # close! (precise value: 9.0)
>>> integrate(math.sin, 0, math.pi, 1000)
1.9999983550656628           # pretty good! (precise value: 2.0)
~~~
> 
> Don't worry about small errors in the rightmost (least-significant) digits. They occur from small differences in `python` versions.
> 
> To get started, here is the "signature" (the def line) and docstring for integrate. Feel free to use this:
~~~text
def integrate(f, low, hi, N):
    """Integrate returns an estimate of the definite integral
       of the function f (the first argument)
       with lower limit low (the second argument)
       and upper limit hi (the third argument)
       where N steps are taken (the fourth argument)

       integrate simply returns the sum of the areas of rectangles
       under f, drawn at the left endpoints of N uniform steps
       from low to hi
    """

assert integrate(dbl, 0, 10, 4) == 75
assert integrate(sq, 0, 10, 4) == 2.5 * sum([0, 2.5*2.5, 5*5, 7.5*7.5])
~~~
This time, we'll try "test-driven development", in which you write the tests first and then make your function satisfy the tests. That's why we included the asserts above! (Note that the second assert is an example of how to test even if you don't know the numerical answer!)
> 
{{% notice tip %}}
Do NOT use a list comprehension: no list is being created here. Rather, use `f_of_fracs` to generate the list of heights you need. Remember that the result of `f_of_fracs` is a big list of `y`-values! You want to multiply those `y`-values (heights) by the rectangles' width. But all the widths are the same! So, you can sum the heights then multiply by the width! Use `python`'s built-in `sum`. `sum(L)` returns the sum of the elements in the list `L`. <br>
{{% /notice %}}
> 
> Some examples of how sum works:
~~~text
>>> sum([10, 4, 1])
15
>>> sum(range(0, 101))
5050
~~~
> 
> If your `integrate` function works, congratulations! You've built a general-purpose routine that can provide integrals for any computable function (including those for which there is no closed-form integral---i.e., ones where the best mathematicians in the world don't know how to compute an exact result).
