---
title: "Threeze"
date: 2018-06-29T07:44:36-04:00
draft: false
weight: 1575
---
 
Background
----------
In Part 1 of this problem you will first build a few basic functions that you'll then use in Part 2 to write a program to solve the Threeze Puzzle.

***Part 1***: The Tools

In this part of the problem you'll write several functions that will be useful in the next part. In the process, you'll build up your "functional programming muscles!"

> `list_to_string(L)`

Write a function called `list_to_string` that takes as input a list of characters and returns the string that results from concatenating these characters. For example
~~~text
>>> list_to_string(["s", "p", "a", "m"])
'spam'
~~~
Your implementation may use recursion, indexing and slicing, and concatenation (concatenation is the `+` symbol) but nothing else!

> `filter(pred, L)`

Python has a built-in function called `filter` that takes two inputs: The first input is a function `pred` that takes as input a single input and returns either `True` or `False`. Such a function is called a *predicate*. The second input is a list `L`. The filter function returns a new list that contains all of the elements of `L` for which the predicate returns `True` (in the same order as in the original list `L`). Consider the example below:

~~~text
# Filename: funcs.py

def even(X):
    if X % 2 == 0:
        return True
    else:
        return False
~~~

~~~
>>> from funcs import even
>>> filter(even, [0, 1, 2, 3, 4, 5, 6])
[0, 2, 4, 6]
~~~

In this example, the predicate `even` returns `True` if and only if its input is an even integer. When we invoke `filter` with predicate `even` and the list `[0, 1, 2, 3, 4, 5, 6]` we get back a list of the even numbers in that list. Of course, the beauty of `filter` is that you can use it with all different kinds of predicates and all different kinds of lists. It's a very general and powerful function! Your job is to write your own version of `filter` called `myfilter`. Your implementation may use recursion, indexing and slicing, and concatenation but no built-in python functions.

> `sublists(L, s)`

In class we wrote the `powerset` function that takes a list `L` as input and returns the list of all sublists of `L`. Recall that a sublist of `L` is a list constructed by simply removing 0 or more elements from `L`. For example, if `L` is the list `[1, 2, 3, 4]` then `[1, 2, 4]`, `[1, 3]`, `[2, 3, 4]`, and `[3, 4]` are among the many sublists of `L`. However, the list `[4, 3]` is not a sublist of `L` because it cannot be obtained by removing elements from `L` (although `[3, 4]` is a sublist of `L`!). Your task here is to write a function called `sublists` that takes a list `L` and a non-negative integer `s` as input and returns the list of all sublists of `L` of length exactly `s`. For example:

~~~text
>>> sublists([1, 2, 3, 4], 2)
[[3, 4], [2, 4], [2, 3], [1, 4], [1, 3], [1, 2]]

>>> sublists([1, 2, 3], 4)
[]
~~~
Notice that in the second case, there are no sublists of `[1, 2, 3]` of length exactly 4, so the set of sublists is empty! Your job is to write the `sublists` function. You may use `len` (which returns the length of a string or list) since we wrote this in class. You may also use `map` since we wrote that in class! Of course, you may use any other function that we've written as well as recursion, indexing and slicing, and concatenation. Nothing else should be used. There are several ways to do this problem!

> `reduce(func, L)`

Python has a built-in function called `reduce` in the `functools` package, which you can use by running the line `from functools import reduce`. Your job is to write your own implementation of this function. `reduce` should take as input two arguments, `func` and `L`. `func` is a function of two variables and `L` is a list of 0 or more items. `reduce` repeatedly applies the function `func` in order to reduce `L` to a single value, which is what is returned by `reduce`.

For example, using the `mult` function we wrote a few days ago, `reduce(mult, [1, 2, 3, 4, 5])` returns the value ((((1*2)*3)*4)*5) = `120`. If `max` is defined as a function of two variables that returns the larger of its two inputs then `reduce(max, [4, 1, 42, 5])` returns `42`.

To complete Part 1, you should have `list_to_string(L)`, `filter(pred, L)`, `sublists(L, s)`, and `reduce(func, L)` all written.

***Part 2***: The Threeze Game

Threeze is a solitaire game played with Scrabble pieces. Here's how it goes: The player draws any number of letters from the Scrabble set and lines them up from left to right on the rack. Representing the rack by a list, we might have a rack that looks like `["b", "c", "a", "n", "r"]`. The objective of the game is write down as many real 3-letter words as possible that can be made from this rack but preserve the left-to-right order of the letters. For example, the words `"ban"`, `"can"`, and `"car"` are all legitimate for this rack. However, `"ran"` is not, since the letters in `"ran"` are not in the same left-to-right order as they appear in the rack. Of course, if we had a rack with fewer than 3 letters, there is no chance that we'll create any 3-letter words!

Your objective is to write a function called `threeze` that takes a list of letters as input (letters may be repeated - you can assume that the user provides a list of letters that she selected from the Scrabble set). `threeze` returns a list of all valid 3-letter words preserving the order in the original list.

How do we determine if a word is valid? Fortunately, we've supplied you with the Official Scrabble Dictionary Player's list of 3-letter words. It's a downloadable list of strings called [ospd3.py](http://www.cs.hmc.edu/~cs5grad/cs5/ospd3.py). Once you've downloaded this file, you can either cut-and-paste it into your file or you can just save it in the same directory as your file and include the line

~~~text
from ospd3 import *
~~~

After running this `import`, you can access the `words` variable, which is a list of strings---each of which is a word!

Your task is to write `threeze`. Here is some sample input and output:

~~~text
>>> threeze(["b", "c", "a", "n", "r"])
['ban', 'bar', 'can', 'car']
>>> threeze(["z", "b", "a", "g"])
['bag', 'zag']
~~~

You may use any function that you've written as part of this assignment as well as the built-in `map` and `filter` functions (since we've written both of these now). You may also use the python `in` syntax. (Recall that the expression `3 in [1, 2, 3]` is `True` since `3` is in the list `[1, 2, 3]`. You can also use `in` on strings: for example, `"s" in "spam"` is also `True`.)

