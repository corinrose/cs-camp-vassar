---
title: "Sequences and Data"
date: 2018-06-14T11:00:04-04:00
weight: 1000
---

Objectives
----------
- Become comfortable working in the `python` interpreter

- Understand common `python` error codes

- Work with indexing and slicing lists and strings

Background
----------

We've already been working with the `python` interpreter the past few exercises. It looks something like this:

~~~text
$ python
Python 3.6.5 (default, May 11 2018, 04:00:52) 
[GCC 8.1.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
~~~
Running `python` in our regular command shell brings up the `python` interpreter (sometimes called the `python` shell, or the `python` interactive console.)

To get started, try a few arithmetic, string, and list expressions in the Python interpreter, e.g.,

~~~text
>>> 40 + 2
42
>>> 40**2
1600
>>> 'hello world!'
'hello world!'
>>> L = [0, 1, 2, 3]
>>> L
[0, 1, 2, 3]
>>> L[0]
0
>>> L[2:]
[2, 3]
>>> [6, 7, 8, 9][1:]
[7, 8, 9]
>>> 2*L
[0, 1, 2, 3, 0, 1, 2, 3]
>>> L == 42
False
>>> L == [0, 1, 2, 3]
True
~~~

Errors and Exceptions
---------------------
Mistakes are unavoidable! So, you'll encounter `python` errors. They're sometimes called *exceptions*, as well.

{{% notice note %}}
One of the most important habits we hope you'll practice in this course is this:
If an error happens, consider it an opportunity, not a problem!
{{% /notice %}}

It's true, in that an error is a chance to:

1. Improve your intuition about how computation works, i.e., the "machine's mindset,"
2. Improve the software you're developing (or your understanding of it), and
3. Build your debugging skills. 

So, let's create some errors, which Python calls *exceptions*:

Give yourself two minutes. In that time, see how many of these `python` exceptions you can cause!

If you create others, all the better---let a coach know, and we'll add them to this list:

- `NameError`  (an unrecognized variable!)
- `TypeError`  (try slicing an integer for example!)
- `ZeroDivisionError`  (perhaps clear from its name)
- `SyntaxError`  (the error that kittens most often produce when walking over the keyboard)
- `IndexError`  (try an out-of-bounds index into a sequence)
- `OverflowError`
    Note that integers won't overflow---if they get too big to fit in memory, they'll simply crash Python. To obtain this error, therefore, you'll need to use a floating-point value, such as 42.0, in some mathematical expression that produces very large values. For example, use the power `**` operator! 

The exercise
----------------------------
This problem will exercise your slicing and indexing skills.

First, create a new text file and save it with the name `sequences.py`.

Then, copy the following starting lines into your new plain-text file:
~~~text
# Vassar CS Camp
# Name: [your name here]
# Filename: sequences.py 

pi = [3, 1, 4, 1, 5, 9]
e = [2, 7, 1]

# Example problem (problem 0):  [2, 7, 5, 9]
answer0 = e[0:2] + pi[-2:]  
print(answer0)
~~~
{{% notice note %}}
Be sure to save this as a plain-text file named `sequences.py`---don't forget the .py extension.
<br>
After the initial comment, this code defines the list named `pi` and the list named `e`.
<br>
When you run the file, the line `answer0 = e[0:2] + pi[-2:]` will define the value held by the variable `answer0`.
<br>
Then, the code will print the value of the variable `answer0`. 
{{% /notice %}}

To run the code:

1. At your command line, make sure you're in the folder where `sequences.py` is saved. Perhaps it's the desktop, or maybe you put it in another folder.
2. Run `python`.

**Composing new lists from `pi`, `e`, and list operations**

The problems below ask you to create several lists using only the list named `pi`, the list named `e`, and these list operations:

- List indexing, such as `pi[0]`
- List slicing, such as `e[1:]`
- Skip slicing, such as `pi[0:6:2]`
- List concatenation with `+`, such as `e[0:2] + pi[-2:]`
  (for this problem, we ask you not to use `+` to add values numerically) 

{{% notice tip %}}
Leave a blank line or two between your answers to keep things readable.
{{% /notice %}}


For fun only, you might try using as few operations as possible, to keep your answers elegant and efficient. 

**Here are the problems**: 

***Problem 0*** Use `pi` and `e` (or just one!) to create the list `[2, 7, 5, 9]`. This is the example above, stored in the variable `answer0`. 

***Problem 1*** Use `pi` and `e` to create the list `[7, 1]`.
  - As above, store this list in the variable `answer1`. Here is a start, to copy and paste:
~~~text
# Problem 1: creating [7, 1]
answer1 =   e[1:2]           # not the right answer, but a start...
print(answer1)
~~~
***Problem 2*** Use `pi` and `e` to create the list `[9, 1, 1]`. Store this list in the variable `answer2`. 

***Problem 3*** Use `pi` and `e` to create the list `[1, 4, 1, 5, 9]`. Store this list in the variable `answer3`. 

***Problem 4*** Use `pi` and `e` to create the list `[1, 2, 3, 4, 5]`. Store this list in the variable `answer4`. 

**String slicing and indexing**

This problem continues in the style of the last one, but uses strings rather than lists.
First, copy these lines into your `sequences.py` file underneath the previous problems (with some blank lines to keep things apart!):
~~~text
# Lab1 string practice

v = 'vassar'
c = 'college'
cs = 'cs camp'
~~~
You may use any combination of these four string operations:

- String indexing, e.g., `v[0]`
- String slicing, e.g., `cs[1:]`
- String concatenation, `+`, e.g., `v + c`
- Repetition, `*`, e.g., `42*v` 

Any correct answer is OK---there's no requirement to use a small number of operations, but see how efficient your solutions can be!

Example problem (#5): Use `v`, `c`, and `cs` to create 'car'. Store this string in the variable `answer5`. We used 3 operations.

Answer to example 5---please copy and paste this into your file:
~~~text
# Problem 5:  'car'
answer5 = c[0] + v[4:6]
print(answer5)
~~~
The 3 operations are 1 use of list indexing, 1 slice, and 1 concatenation with `+`.

Here are the string-creation challenges (and, in parentheses, our most efficient answers, at least so far):

Remember that the "most efficient" answers are not at all needed (they may be fun, but any working answer is 100% OK!) 

***Problem 5*** (The example from above)    Create `car` and store this string in the variable `answer5`. 

***Problem 6*** Create `collage` and store this string in the variable `answer6`. 

***Problem 7*** Create `assarollege` and store this string in the variable `answer7`. 

***Problem 8*** Create `vassvassvass` and store this string in the variable `answer8`. 

***Problem 9*** Create `lovelegos` and store this string in the variable `answer9`.

***Problem 10*** Create `clearcall` and store this string in the variable `answer10`. 
