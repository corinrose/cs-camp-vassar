---
title: "Four Fours"
date: 2018-06-14T10:04:14-04:00
weight: 750
---

Objectives
----------
 - Meet the Python interactive console
 - Introduce working with Python files

Background
----------
Finally time for Python! Python is a general-purpose programming language, which
just means it can do a lot of things -- way more than Picobot. It's a very
flexible language with readable syntax, powerful abstraction, and widespread
use. Knowing Python is an incredibly practical skill and can be used in so many
different areas: data science, video game development, dev ops (scripting), web
development, and many more (too many to list). If you have a use in mind, come
talk to any of us about it!

Over the next few days, we'll be going through concepts in Python that will be
the tools in your programmer toolbelt.

Getting Started
---------------
One of the great features of Python is its **interactive console**. We'll be
referring to it just as "console" for brevity. Try opening it up either in the
terminal or [directly in
vscode](https://cscamp.cs.vassar.edu/exercises/using_vscode)! When you're in
your terminal of choice, type `python` and hit <kbd>Enter</kbd>. You should see
something like this, with your cursor positioned right after the `>>>`:

~~~text
$ python

Python 3.5.2 (default, Nov 23 2017, 16:37:01)
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
~~~

{{% notice warning %}}
Make sure it doesn't say Python 2.7.12 or any version of Python starting with a 2. It is an old version of Python. You should not use it!
{{% /notice %}}

Try a simple computation:

~~~text
>>> 6*7
42
~~~

Not let's try computing a power. Python uses `**` as the power operator.

~~~text
>>> 10 ** 100
10000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
~~~

Careful trying any larger computations. You might crash Python!

{{% notice tip %}}
If you find yourself in a scenario where you've hit <kbd>Enter</kbd> after
typing something in either the Python console or terminal and something goes
wrong, try hitting <kbd>Ctrl</kbd>+<kbd>C</kbd> a few times (hitting multiple
times can matter in some cases). It tells the computer to stop whatever it's
doing and bring back a prompt.
{{% /notice %}}

Try copying the following into the terminal (in vscode or not).

~~~text
>>> print("Zero is", 4 + 4 - 4 - 4)
Zero is 0
~~~

We used four fours to make zero. We're going to do this a bunch more in this
exercise. But we don't want to have to paste in a line of code every time we
want to execute it. So, before we get to the exercise itself, let's talk about
how to create a Python file to store your code for easy editing and executing.

In previous exercises, we've done the following to make new text files. Note the
`$` prompt indicating we're in the terminal -- not the Python console.

~~~text
$ code some_text_file.txt
~~~

To make a Python file, we'll do the same thing except instead of `.txt` we'll
append `.py` to the filename. If you're already using the vscode terminal, you
can just use the menu to make a new file. Otherwise:

~~~text
$ code some_python_file.py
~~~

{{% notice info %}}
In reality, both `.txt` and `.py` files both just contain characters (letters,
symbols, etc), but the **file extension** allows the Python interpreter to
recognize a file as having Python in it. You can think of a file extension as a
label to help your computer figure out how to handle a particular file. Don't
worry too much about what a Python interpreter is. If you think of code as
instructions, the Python interpreter is who you're instructing.
{{% /notice %}}

Now, paste the following code into your file and **save it**.

~~~
# Vassar CS Camp
# Filename:
# Name:

from math import *

print("Zero is", 4 + 4 - 4 - 4)
~~~

Back in your terminal, navigate using `cd` to wherever you saved your file. You
want your working directory to be the directory that contains the `.py` file you
just saved. Once you're there, enter the following replacing `[your-file-name]`
with whatever you saved your file as:

~~~text
 $ python [your-file-name]
Zero is 0
~~~

Make sure you have the `.py` on the end!

{{% notice tip %}}
Tab completion is your friend! When you press <kbd>Tab</kbd> while typing in the
terminal, it will try and finish what you're typing for you. It knows the entire
structure of your filesystem, so whether you're typing the name of a file in
your working directory or typing a long path, it can finish long names for you.
If nothing shows up on the first press, hit <kbd>Tab</kbd> again and a list of
possible autocompletions will print out. It will only every complete a word if
what you've typed is the prefix of exactly one item in the relevant directory.
{{% /notice %}}


> The Exercise
> ------------
> For the exercise, we'll be adding more lines to this file. Remember to **save**
> after every addition -- namely before you try and run the code (using `python`
> in the terminal). Otherwise, it will run the code you had at your last save. See
> [the previous exercise about
> vscode](https://cscamp.cs.vassar.edu/exercises/using_vscode) to turn on
> auto-saving!
> 
> The goal is to use four fours in a mathematical expression to produce every
> integer value between 0 (which we already did) and 20. You can use the following
> operators:
> 
>  - `+` (addition)
>  - `-` (subtraction)
>  - `*` (multiplication)
>  - `/` (division)
>  - `(` `)` (grouping)
>  - `**` (power/exponential)
>  - `sqrt(x)` (square root of x)
>  - `factorial(x)` (factorial of x)
> 
> Right now your program only prints one line, but a complete program will print
out the following:
> 
~~~text
Zero is 0
One is 1
Two is 2
Three is 3
Four is 4
Five is 5
Six is 6
Seven is 7
Eight is 8
Nine is 9
Ten is 10
Eleven is 11
Twelve is 12
Thirteen is 13
Fourteen is 14
Fifteen is 15
Sixteen is 16
Seventeen is 17
Eighteen is 18
Nineteen is 19
Twenty is 20
~~~
> 
{{% expand Hint %}}
The power operator ( `**` ) is a very useful tool in this exercise. Also, try
and repurpose subexpressions from previous answers to help solve ones you
haven't yet.
{{% /expand %}}
> 
> Feel free to do more than 20 if you're so inclined! And remember to ask for help if you're stuck!
>  
> May the fours be with you.
