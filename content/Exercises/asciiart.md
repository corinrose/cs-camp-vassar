---
title: "Ascii Art"
date: 2018-06-27T09:38:24-04:00
weight: 1800
draft: false
---

Objectives
----------
 - Get more comfortable with nesting loops

Background
----------
Before modern graphics were feasible, a lot of visuals were creating using just text. You can take a look at some examples [here](https://www.asciiart.eu/).

{{% notice note %}}
Do not use string multiplication (`'hi' * 3`) to solve these problems. The only valid use of string multiplication is to create spacing (`' ' * 5`), e.g. in the `printDiamond` function.
{{% /notice %}}

Exercises
---------

{{% notice tip %}}
To get spaces between the characters that make up your shapes, you can simply append a space character to the passed symbol(s) before printing anything. The right-most characters will have a trailing space, but we're going to rely on the fact that they're invisible and ignore them.
{{% /notice %}}

***Problem 1*** Write the `printRect` function.

`printRect` takes three arguments (`width`, `height`, `symbol`) and prints a `width`-by-`height` rectangle of `symbol`s.

Here is some example output:

~~~text
>>> printRect(4, 6, '%')
% % % % 
% % % % 
% % % % 
% % % % 
% % % % 
% % % % 

>>> printRect(0, 4, '%') # print 4 blank lines





>>> printRect(2, 7, '') # prints 7 blank lines
  
  
  
  
  
  
  

>>> printRect(6, 1, '!')
! ! ! ! ! ! 
~~~

***Problem 2*** Write the `printTri` function.

`printTri` takes three arguments (`width`, `symbol`, `rightSideUp`) and prints a right triangle of `symbol`s whose legs are `width` long. `rightSideUp` is a Boolean that determines whether the triangle is upside-down or not.

Here is some example output:

~~~text
>>> printTri(3, '@', True)
@ 
@ @ 
@ @ @ 

>>> printTri(3, '@', False)
@ @ @ 
@ @ 
@ 

>>> printTri(0, '@', False) # prints nothing

>>> printTri(6, '', True) # prints 6 blank lines
 
  
   
    
     
      
~~~

***Problem 3*** Write the `printBumps` function.

`printBumps` takes three arguments (`num`, `symbol1`, `symbol2`) and prints `num` successively larger bumps, starting with a height of 1.

{{% notice tip %}}
Do you see any triangles inside the bumps?
{{% /notice %}}

~~~text
>>> printBumps(3, '%', '#')
% 
# 
% 
% % 
# # 
# 
% 
% % 
% % % 
# # # 
# # 
# 

>>> printBumps(3, '@', '')
@ 
 
@ 
@ @ 
  
 
@ 
@ @ 
@ @ @ 
   
  
 
~~~

***Problem 4*** Write the `printDiamond` function.

`printDiamond` takes two arguments (`width`, `symbol`) and prints a `width`-wide diamond of `symbol`s.

Here is some example output:

~~~text
>>> printDiamond(3, '#')
  # 
 # # 
# # # 
 # # 
  # 

>>> printDiamond(1, '@')
@

>>> printDiamond(5, '$')
    $ 
   $ $ 
  $ $ $ 
 $ $ $ $ 
$ $ $ $ $ 
 $ $ $ $ 
  $ $ $ 
   $ $ 
    $ 
~~~

Optional Bonus Challenge
------------------------

In the following problems, we are going to use a list of lists to represent a 2D grid. Elements in the outer list are lists that represent the rows, and elements in the inner lists are the data that populates each row (and therefore the whole grid). The data in the inner lists, in this case, are symbols that we'll be printing on the screen. For example, we could change the `printRect` function to return a list of lists rather than print immediately.

***Problem 1*** Rewrite `printRect` as `genRect`. `genRect` takes the same arguments, but instead of printing to the screen, returns a list of lists that corresponds to what `printRect` would've printed.

~~~text
>>> genRect(1, 2, '$')
[['$'], ['$']]

>>> genRect(4, 6, '%')
[['%', '%', '%', '%'], ['%', '%', '%', '%'], ['%', '%', '%', '%'], ['%', '%', '%', '%'], ['%', '%', '%', '%'], ['%', '%', '%', '%']]
~~~

***Problem 2*** Write the function `display(L)` that prints a list of lists `L`. Remember each inner list (i.e. an element of the outer list `L`) represents a row. That is, the first element in `L` is a list of characters that corresponds to the first row of the ascii art to be printed. Unlike previously, **don't** print a space between each character.

~~~text
>>> display([['@', '@', '@'], ['#', '#', '#'], ['%', '%', '%']])
@@@
###
%%%
~~~

The following two should have equivalent behavior:

> `printRect(4, 6, '%')`
> <br>
> `display(genRect(4, 6, '%'))`


***Problem 3*** Write an `animate(frames)` function that takes one argument (`frames`) that is a list containing list of lists and continuously `display`s the elements of `frames` in order, over and over. In between each frame, use `time.sleep(s)` to pause for `s` seconds. Remember, you'll need to import the time package to do so.

~~~text
import time

time.sleep(0.1) # pauses for 0.1 seconds
~~~

Print some large number of blank lines right before you print each frame, as well. This is just to make the animation easier to look at in the terminal. It might be a good idea to run this file in a standalone terminal (outside of vscode) for easier viewing.

~~~text
print('\n' * 50)
~~~

When you have your functions written, try running the following:

~~~text
L1 = [list('   _______'), list('x---(###)'), list('     ~ ~')]
L2 = [list('      |   '), list('+---(#|#)'), list('     ~ ~')]
animate([L1, L2])
~~~

Try making your own little animation, too!
