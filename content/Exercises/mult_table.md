---
title: "Multiplication Table"
date: 2018-07-02T09:46:30-04:00
draft: false
weight: 1700
---

In this exercise, you will write a `mult_table` function which will take in a single positive whole number `dim` (for dimension) and print out a multiplication table of that size. For example,

~~~text
>>> mult_table(10)
 1  2  3  4  5  6  7  8  9 10 
 2  4  6  8 10 12 14 16 18 20 
 3  6  9 12 15 18 21 24 27 30 
 4  8 12 16 20 24 28 32 36 40 
 5 10 15 20 25 30 35 40 45 50 
 6 12 18 24 30 36 42 48 54 60 
 7 14 21 28 35 42 49 56 63 70 
 8 16 24 32 40 48 56 64 72 80 
 9 18 27 36 45 54 63 72 81 90 
10 20 30 40 50 60 70 80 90 100 
~~~

As you can see, the multiplication table takes every number up to and including the input and multiplies it by every other number in that same range. 

There are lots of ways to do this, but a good way to start is by using a nested `for` loop---that is, a `for` loop within another `for` loop. You can define an empty string before this loop and add each line of numbers to it---recall that you can convert a number `n` to a string with `str(n)`. After each line is complete, you can add `"\n"` to the string, which represents a new line. Then, once you have constructed this string, you can print it out all at once at the end of your function!

You can space the numbers out properly by writing an `if` statement which checks if the current number is less than 10 and if so, adds an extra space to the string so this number is the same width as two digit numbers. This is sufficient to complete this problem, but note that this method will only work for `dim` up to 10!

**Bonus**

If you want to make this multiplication table better, you can use the `log10(x)` function from the `math` package. Recall that if you wish to use this function, you can write `from math import log10` at the top of your program.

`log10(x)` (pronounced "log base 10 of x") is the inverse function of `10**x`---in other words, `log10(10**x) == x` is always `True`. `log10(x)` can be thought of as the number you would raise 10 to to get *x*. Thus, `log10(10)` is 1, `log10(100)` is 2, and `log10(sqrt(10))` is 1/2. Conveniently, since our numbers have a base of 10, we see that if we plug a number in to `log10` and round the result down, it will tell give us the number of digits in our number minus one. 

So, we can easily write a `get_digits(n)` function which uses `log10` to calculate the number of digits in `n`, and then we can use this function to make our multiplication table dynamically scale so that each number has the correct amount of spacing, regardless of how big our numbers are!

