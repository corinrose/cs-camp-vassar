---
title: "Recursion Challenges"
date: 2018-06-26T10:02:48-04:00
draft: false
weight: 1350
---
***Problem 1*** Write the recursive function `rep_letter`.

The `rep_letter` function takes in a string `S` and a number `rep` as input and returns a string resulting from repeating each character of `S` `rep` times. Here are some examples:

~~~text
>>> rep_letter('hello', 3)
'hhheeellllllooo'

>>> rep_letter('123', 5)
'111112222233333'

>>> rep_letter('', 10000)
''
~~~

***Problem 2*** Write the recursive function `pal_checker`.

The `pal_checker` function takes in a string `P` as input and returns a boolean corresponding to whether `P` is a palindrome or not.

{{% notice note %}}
You can assume P will only contain lowercase letters `a`-`z`.
{{% /notice %}}

Remember, a palindrome is (in our case) a string that reads the same forwards and backwards. It is therefore true that the first and last characters of a palindrome are the same -- as are the next two characters inside those and so on.

~~~text
>>> pal_checker('palindrome')
False

>>> pal_checker('kayak')
True

>>> pal_checker('a')
True

>>> pal_checker('')
True
~~~

***Problem 3*** Write a recursive funcion `gcd`.

This function should take in two numbers, `x` and `y`, and calculate the *greatest common divisor* of these numbers. That is, the largest number that divides both `x` and `y`.

We can accomplish this using the Euclidian Algorithm, which says that greatest common denominator of `x` and `y` is the same as the greatest common denominator of `y` and `x % y`, the remainder when `x` is divided by `y`.

{{% notice tip %}}
Note that `gcd(x, 0) = x`. This is because *any* number is a divisor of 0, and the greatest divisor of `x` is itself---thus, the greatest common divisor of `x` and 0 is `x`!
{{% /notice %}}

~~~text
>>> gcd(102, 68)
34
>>> gcd(1066, 904)
2
>>> gcd(270, 192)
6
~~~
