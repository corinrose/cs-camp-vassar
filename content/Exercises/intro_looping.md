---
title: "Introduction to Looping"
date: 2018-06-27T09:50:08-04:00
draft: false
weight: 1600
---

Objectives
----------
- Learn how to write loops
- Understand how loops differ from and are similar to recursion


Looping `for` a `while`...
----------------------
Repetition is what computers do best---and what people enjoy not having to do!

To get into the design mindset of using loops, paste this function (and comments) into a new file named `loops.py`. This is a factorial function that uses a `python` `for` loop:

~~~text
# Vassar CS Camp 
# Name: [your name here]
# Filename: loops.py

def fac(n):
    """Loop-based factorial function
       Argument: a nonnegative integer, n
       Return value: the factorial of n
    """
    result = 1                 # starting value - like a base case
    for x in range(1,n+1):     # loop from 1 to n, inclusive
        result = result * x    # update the result by mult. by x
    return result              # notice this is AFTER the loop!

#
# Tests for looping factorial
#
assert fac(0) == 1
assert fac(5) == 120
~~~

**Problem 1**: `power(b,p)`

To start, read over and run the above starter file. You should see the tests pass with the expected results.

Then, either copy and alter that function, or create a new function, based on that model, named `power(b, p)`, which should

- Accept any numeric value (base) `b`
- Accept any nonnegative integer (power) `p`   (`p` can be 0)
- Return the value of `b**p`.
- The function must use a `for` loop! (writing return `b**p` is not in the spirit of this practice...)
- For this problem, `power(0, 0)` should return 1.0   (we realize this might push some mathematicians' tolerance past its limit) 

Here are a few tests to paste and use.
~~~text
print("power(2, 5): should be 32 ==", power(2, 5))
print("power(5, 2): should be 25 ==", power(5, 2))
print("power(42, 0): should be 1 ==", power(42, 0))
print("power(0, 42): should be 0 ==", power(0, 42))
print("power(0, 0): should be 1 ==", power(0, 0))
~~~
{{% notice tip %}}
The value of `n` in factorial is analogous to the value of `p` (the power) in the power function. (The base is simply used as the multiplied value...)
{{% /notice %}}


**Problem 2**: `summed_odds(L)`

Here is a loop-based summed function we looked at---or will look at---in class. Include this in your file (and try it out):
~~~text
def summed(L):
    """Loop-based function to return a numeric list.
       ("sum" is built-in, so we're using a different name.)
       Argument: L, a list of integers.
       Result: the sum of the list L.
    """
    result = 0
    for e in L:
        result = result + e    # or result += e
    return result

# tests!
assert summed([4, 5, 6]) == 15
assert summed(range(3, 10)) == 42
~~~

Either by using this as a template or by copy-paste-and-alter, create a loop-based function named `summed_odds(L)`, which should

- Accept any list of integers L.
- You may assume it includes only integers.
- It should return the sum of all of the odd elements in L
- ...using a loop! 

{{% notice tip%}}
Use an `if` statement inside the loop and only add to result under the correct conditions
{{% /notice %}}

**Problem 3**: `until_a_repeat(high)`

This function will let you explore what is sometimes called the birthday paradox:

- Even in a very small group of people (23 or more), there is greater than a 50-50 chance that a pair of those people share a birthday.
 - This is explained well [here](https://betterexplained.com/articles/understanding-the-birthday-paradox/), including a nice discussion of why it seems paradoxical. 

First, paste and try out the number-guessing `while`-loop example from class:

~~~text
import random

def count_guesses(hidden):
    """Uses a while loop to guess "hidden", from 0 to 99.
       Argument: hidden, a "hidden" integer from 0 to 99.
       Result: the number of guesses needed to guess hidden.
    """
    guess = random.choice(range(0, 100))     # 0 to 99, inclusive
    numguesses = 1                           # we just made one guess, above
    while guess != hidden:
        guess = random.choice(range(0, 100)) # guess again!
        numguesses += 1                      # add one to our number of guesses
    return numguesses
~~~

Then, using `countGuesses` as a starting point (feel free to copy and alter it), write a variant of this function named `until_a_repeat(high)`, which

- Keeps a list `L` of all of the integers guessed. Start with `L = []`!
- Keeps looping as long as all of the elements in `L` are unique (no repeats).
  - Use a `while` loop!
  - Use the `unique(L)` function that's provided below---it returns a Boolean. 
- Within the `while` loop:
  - Make a guess in the `range(0, high)`.
  - Count the number of guesses (add one each time to some kind of counting variable).
  - Add the guess on to the end of the list `L` (see below for a hint on this...). 
- When the `while` loop finishes, the function should return the number of guesses needed until it gets a repeat. 


**Hints**:

- Remember that you can add 1 to a variable with `count += 1`
- Similarly, you can add a new element 42 to the end of a list `L` with the line
    `L = L + [42]`
- The element needs to be in brackets, because only lists can be added to lists.

- Feel free to use this `unique(L)` function provided here.
~~~text
    def unique(L):
      """Returns whether all elements in L are unique.
         Argument: L, a list of any elements.
         Return value: True, if all elements in L are unique,
                    or False, if there is any repeated element
      """
      if len(L) == 0:
        return True
      elif L[0] in L[1:]:
        return False
      else:
        return unique(L[1:])  # recursion is OK in this function!
~~~

Once you've written your `until_a_repeat` function, you should confirm that `until_a_repeat(365)` produces surpringingly small numbers! For example,
~~~text
>>> until_a_repeat(365)
25
>>> until_a_repeat(365)
8
>>> until_a_repeat(365)
23
>>> until_a_repeat(365)
33
~~~

...and then try running 10,000 times with a list comprehension:
~~~text
L = [until_a_repeat(365) for i in range(10000)]
~~~

You might find the average, maximum, and minimum of that list comprehension `L`:
~~~text
>>> sum(L)/10000

>>> max(L)

>>> min(L)

>>> 42 in L
~~~
See if these values match your intuition.

Sometimes it's tricky to know whether it's one's program---or intuition---that needs refinement!

Optional Bonus Challenge
------------------------
***Problem 1*** Write the `integer_div` function. This function takes two arguments (`numer`, `denom`) and returns the result of performing integer division like so: `numer // denom`. You cannot use floating point division ( `/` ) or integer division ( `//` ) in your implementation.

Here is some example output:

~~~text
>>> integer_div(10, 3)
3

>>> integer_div(0, 53)
0

>>> integer_div(16, 7)
2
~~~

{{% notice warning %}}
What happens in your function when you try to divide by 0?
{{% /notice %}}

***Problem 2*** Write the `my_mod` function. This function takes two arguments (`numer`, `mod`) and returns the result of performing mod like so: `numer % mod`. You cannot use the mod operator ( `%` ) or any division ( `/` or `//` ) in your implementation.

Here is some example output:

~~~text
>>> my_mod(10, 3)
1

>>> my_mod(0, 53)
0

>> my_mod(16, 7)
2
~~~

