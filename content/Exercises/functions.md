---
title: "Function Fun"
date: 2018-06-14T14:31:07-04:00
weight: 1100
---

Objectives
----------
- Become familiar with using built-in `python` functions

- Learn the syntax for defining functions

Background
----------

Often, we end up in situations where we need to write multiple pieces of code that do the same thing to different data. For example, we have a list of numbers and we want to get a list of the squares of each of these numbers plus 10, we will need to repeat the code squaring the number and adding 10 for each item.
Functions let us define reusable blocks of code abstractly, with no reference to specific data. Then, we can pass all of these numbers into our function and it will know to square them and add 10.

Using built-in functions
------------------------

First, try out some of `python`'s many built-in functions. Begin by loading up the interactive console by entering `python` in your command shell.

We can now use some built-in functions like `sum()`.

~~~text
>>> L = [0, 1, 2, 3]
>>> sum(L)
6
~~~

We can see that `sum()` takes in a list of numbers and returns the sum of it's elements.

In the same console, we can use `len()`, which returns the length of its input, such as a string or a list.

~~~text
>>> len(L)
4
~~~

Importing from modules
----------------------

To access functions that are not built in by default, you need to load them from their modules or libraries. (We use those terms interchangeably.) Try out these examples to get familiar with how to access `python`'s many libraries:

You can import a module, i.e., a library, and then access its functions with that module name:
~~~text
>>> import math
>>>
~~~

Now, we can access a ton of math related functions! For example,

~~~text
>>> math.sqrt(9)
3.0
>>> math.cos(3.14159)
-0.9999999999964793
~~~

Tired of typing math. in front of things? You can avoid this with
~~~text
>>> from math import *
~~~
The asterisk `*` here means "everything." This will bring all of the functions and constants from the `math` module into your current `python` environment---and now you can use them without prefacing them with `math.`!
~~~text
>>> cos(pi)
-1.0
~~~
This would have had to be `math.cos(math.pi)` if we had done `import math` instead of `from math import *`.

{{% notice warning %}}
It's not always the best idea to import everything with an `*` like this, especially when you're using lots of libraries---some libraries may share the same function or variable name, or you may have defined a function or variable in your own code with the same name as one you are trying to import.
{{% /notice %}}

Writing our own functions
-------------------------
Next, you'll create a few functions of your own in a new file, `ex11.py`.

So, use your text-editor to create a new file named `ex11.py`.

{{% notice note %}}
Throughout the course, we will cover functions in detail. Here, in anticipation, you'll create a few functions just to get started.
{{% /notice %}}

Functions are the fundamental building blocks of computation. What distinguishes `python` from other computing environments is the ease and power of creating your own functions!

Start by pasting the following comments and a definition of a function named `dbl`:

~~~text
# Vassar CS Camp
# Name: [your name here]
# Filename: ex11.py 

def dbl(x):
    """Result: dbl returns twice its argument
       Argument x: a number (int or float)
       Spam is great, and dbl("spam") is better!
    """
    return 2*x
~~~

Now you can use this function in the interactive console as usual by running `python` in your command shell and entering `from ex11 import dbl`. Then, we can use the `dbl()` function from the interactive console!
~~~text
>>> dbl(2)
4
>>> dbl('wow! ')
'wow! wow! '
~~~

**Signature and Docstring**

The first line of a `python` function is called its ***signature***. The function signature includes the keyword `def`, the name of the function, and a parenthesized list of arguments to the function.

Directly underneath the signature is a string inside triple quotes `"""`---this is called the ***docstring***, short for "documentation string." We ask you to include a docstring in all of your functions (even simple ones such as these, so that you will develop the habit early on).

A docstring should describe the function's arguments and result (return value). As you see above, it may include other important information, too. Docstrings are how your functions become part of `python`'s built-in help system.

To see this, type

~~~text
>>> help(dbl)
~~~

and you will see that `python` provides the docstring as the help! The language's help system is docstrings! This self-documenting feature in Python is especially important for making your functions understandable, both to others and to yourself.

{{% notice warning %}}
The first set of triple quotes of a docstring needs to be indented underneath the function definition def line, at the same level of indentation as the rest of block of code that defines the function. 
{{% /notice %}}

**Writing your own functions...**

Let's go!

For each of these functions, be sure to include a docstring that describes **what your function does** and **what its arguments are** for each function. See the `tpl` example, below, for a reasonable starting point and guide:

> **Example problem**: Write the function `tpl(x)`, which accepts a numeric argument and returns three times that argument.

> **Answer to example problem**: Copy the following solution (after a few blank lines to leave space and help readability) into your ex11.py file:
~~~text
def tpl(x):
    """Return value: tpl returns thrice its argument
       Argument x: a number (int or float)
    """
    return 3*x
~~~

<br>

The exercise
------------
You have five functions to write.

***Problem 1*** Write `sq(x)`, which accepts a numeric argument named `x`. Then, `sq` should return the square of its argument.
Note that this is the square, not the square root. (The square is x times itself...)

***Problem 2*** `interp(low, hi, fraction)` accepts three numbers as its arguments: `low`, `hi`, and `fraction`, and should return the floating-point value that is `fraction` of the way between `low` and `hi`.

**What!?**

That is to say, if `fraction` is zero, `low` will be returned. If `fraction` is one, `hi` will be returned, and values of `fraction` between 0 and 1 will lead to results between `low` and `hi`. (In fact, values of `fraction` can go below 0, yielding return values less than `low`, and they can go above 1, producing return values greater than `high`. Purists would call this extrapolation, rather than interpolation, however.)

From the above description, it might be tempting to divide this function into several cases and use `if`, `elif`, and the like. Yet, this function can be written using no conditional (`if`/`elif`/`else`) constructions at all! Try it without using `if`!

As noted, your function should also work if `fraction` is less than zero or greater than one. In this case, it will be linearly extrapolating, rather than interpolating. We'll stick with the name `interp` anyway.

Here are examples that will help clarify how `interp` works:
~~~text
>>> interp(1.0, 9.0, 0.25)      # A quarter (.25) of the way from 1.0 to 9.0
3.0
>>> interp(1.0, 3.0, 0.25)      # A quarter of the way from 1.0 to 3.0
1.5
>>> interp(2, 12, 0.22)         # 22% of the way from 2 to 12
4.2
~~~

{{% notice tip %}}
If you're unsure of where to begin on this problem, look at the first example above. In it
low is 1.0 
hi is 9.0 
fraction is 0.25 
See if you can determine how to combine those three values to yield the correct return value of 3.0. (Consider starting with (hi - low).)
{{% /notice %}}

Here are two more examples to try:
~~~text
>>> interp(24, 42, 0)           # 0% of the way from 24 to 42
24.0
>>> interp(102, 117, -4.0)      # -400% of the way from 102 to 117 (whoa!)
42.0
~~~

The next several functions involve strings of characters. Write each one in your ex11.py file. After you write each function, be sure to test it before moving on to the next one! Also, be sure to include a docstring for each function that tells (very briefly) what it does.

***Problem 3*** Write a function `checkends(s)`, which takes in a string `s` and returns `True` if the first character in `s` is the same as the last character in `s`. It returns `False` otherwise. The `checkends` function does not have to work on the empty string (the string `''`).
There is a hint below, but read through the examples first.
These examples will help explain `checkends`---read them over now, and be sure to try them once you have a first draft of your function. Notice that the final, fourth example below is the string of one space character, which is different from the empty string, which contains no characters:
~~~text
>>> checkends('no match')
False
>>> checkends('hah! a match')
True
>>> checkends('q')
True
>>> checkends(' ')
True
~~~
Make sure to check that this last example (the string of a single space) works for your `checkends` function. The empty string does not need to work.

{{% notice tip %}}
For this function you could use an if and else construction... here is a start:
~~~
if s[0] == ______ :
    return True
else:
    return False
~~~
{{% /notice %}}

You might find a solution that doesn't use the if and else at all---this is fine, too. (Hint: the comparison x == 42 is an expression that evalutes to either True or False.) Notice that the last character is missing above---you'll need to fill that in!

{{% notice warning %}}
Your function should not return strings! Rather, it should return a Boolean value, either `True` or `False`, without any quotes around them. These `True` and `False` are keywords recognized by `python` as representing one bit of information.
You'll see these Booleans turn a different color, blue in vscode's default color scheme, indicating that `python` recognizes them as bool values. (If you'd accidentally made them strings, they'd be quoted, and they'd be orange in vscode.) In sum, Booleans and strings are different. For `True` and `False` you would almost always want the unquoted Boolean values.
{{% /notice %}}

***Problem 4*** Write a function `flipside(s)`, which accepts a string `s` and returns a string whose first half is `s`'s second half and whose second half is `s`'s first half. If `len(s)` (the length of s) is odd, the "first half" of `s` is considered to have one fewer character than the second half. (Accordingly, the second half of the returned string will be one shorter than the first half in these cases.) There's also a hint after the examples below.
Here you may want to use the built-in function `len(s)`, which returns the length of its argument string, `s`.

Examples:
~~~text
>>> flipside('homework')
workhome
>>> flipside('carpets')
petscar
~~~
This function is simpler if you create a variable equal to `len(s)//2` on the first line, e.g.,
~~~text
def flipside(s):
  """put your docstring here
  """
  x = len(s)//2
  return_____________
~~~
where the return statement has been left up to you. It will use the variable `x` twice, which is why it's nice to give it a name, rather than type and re-type it!

{{% notice note %}}
`len(s)//2` takes `len(s)`, divides it by `2`, and rounds the result down to the nearest integer.
{{% /notice  %}}

{{% notice note %}}
The name `x` is a pretty poor one in this case; `l` (for "length") might be better. We didn't suggest `l` because it looks too much like the number `1`. What name might be better than `x`? Remember that `python` allows multi-letter names, and that `len` is already used!
{{% /notice %}}

***Problem 5*** Write `convert_from_seconds(s)`, which takes in a nonnegative integer number of seconds `s` and returns a list (we'll call it `L`) of four nonnegative integers that represents that number of seconds in more conventional units of time, such that:

- The initial element represents a number of days
- The next element represents a number of hours
- The next element represents a number of minutes
- The final one represents a number of seconds

You should be sure that

- 0 <= seconds < 60
- 0 <= minutes < 60
- 0 <= hours < 24

There are no limits on the number of days.
For instance,
~~~text
>>> convert_from_seconds(610)
[0, 0, 10, 10]
convert_from_seconds(100000)
[1, 3, 46, 40]
~~~
*How to do this?*
Feel free to copy and paste this starter code that uses four variables:
~~~text
def convertFromSeconds(s):
  days = s // (24*60*60)  # Number of days
  s = s % (24*60*60)      # The leftover
  hours = 
  minutes = 
  seconds = 
  return [days, hours, minutes, seconds]
~~~

The idea here is that when those four variables are all correctly set, you can return them all in a list, which is the final line:
~~~text
return [days, hours, minutes, seconds]
~~~
For instance, the line that sets days is
~~~text
days = s // (24*60*60)
~~~
What would be other lines be?
It's possible to do this without changing the variable `s` at all. However, as the above starting code suggests, it's also possible to alter `s` as you go. Try this latter approach, just to get the hang of this powerful strategy.

**Problem 6** Add functions to your RPS game! To start, define a `help` function that when called prints out some information about how to play rock, paper, scissors. At any point in the game, if the user enters "help" (say, instead of entering their choice of rock, paper, or scissor), use the function to print out helpful information. If you need, here's some code to get you started with your help function:

~~~text
def rps_help():
    """prints help information about how to play RPS"""

	print('helpful information')
~~~

Optional bonus challenge
------------------------
***Problem 1*** Add a `get_move` function that calls `input` to get the user's choice of rock, paper, or scissors. It checks that what they entered is valid before returning it. It should act just like `input` except return something that you know means the user typed something invalid. That could be, for example, the string `'invalid'`, and when you use `get_move` in your RPS game, in addition to checking for `'rock'`, `'paper'`, and `'scissors'`, check for `'invalid'`. If your `rps` function sees the `'invalid'` returned by your `get_move` function, it should do nothing and ask for input again (using `get_move`) because the `get_move` function will handle it.

You should have your `get_move` function handle printing a help message (i.e. calling your `help` function) if the user inputs help as well as printing a message about invalid input.

~~~text
def get_move(prompt):
    """calls input to get RPS move from user and validates it"""

    choice = input(prompt)

    # validate the response here

    return choice
~~~
