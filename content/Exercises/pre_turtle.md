---
title: "Python Turtles"
date: 2018-06-22T06:07:52-04:00
weight:  1150
---

Objectives
----------
- Practice writing functions using turtles

Background
----------
Now that we've learned to write our own functions, let's tell a turtle what to do! We'll be using the turtle package that's built into Python to practice writing some functions. For reference, [here](https://docs.python.org/3.3/library/turtle.html?highlight=turtle#overview-of-available-turtle-and-screen-methods) is some turtle package documentation.

Getting Set Up
--------------
All your code from this exercise should go in a file called `my-turtle.py`. Before adding any of your own code, we need to get access to the turtle package, so we can use the turtle functions.

Add this line at the very beginning:

~~~text
import turtle
~~~

This gives us access to any functions defined in the turtle package by prepending `turtle.` to the function name when we call it (note the dot). For example, if we want to use the `forward` function to make the turtle move forward a specified distance, we would write `turtle.forward(25)` to move the turtle forward by 25 units. Here are a list of useful turtle functions that you might use:

- `forward(d)` and `backward(d)` move the turtle forward or backward by `d` distance
- `right(a)` and `left(a)` turn the turtle right or left by `a` degrees
- `speed(s)` sets the speed of the turtle to an integer value `s` between 0 and 10 (see [the docs](https://docs.python.org/3.3/library/turtle.html?highlight=turtle#turtle.speed) for what the numbers mean)
- `circle(r)` draws a circle *to the left* of the turtle with radius `r`.

Here's an example that makes the turtle walk forward, turn around, and walk forward again (returning to where it started).

~~~text
import turtle

turtle.forward(100) # move forward 100 units
turtle.right(180)   # turn around
turtle.forward(100) # move forward 100 units again
~~~

When you want to test any functions in your file, you'll need to do so in a Python interactive console. After you open it up, import your file (slightly differently than we just did with turtle) by entering the following:

~~~text
>>> from my-turtle import *
~~~

> We'll talk about the differences between these two ways of importing at the beginning of the *Getting Started* section.)

Then, just call the function you want to see. If you want to see your `flower` function (which you will write by the end of this exercise), enter:

~~~text
>>> flower()
~~~

It should pop open a graphics window and your turtle will move as described in your function.

You can type:

~~~text
>>> clear()
~~~

to clear the screen and

~~~text
>>> home()
~~~

to bring the turtle back to where it started.

Getting Started
---------------
{{% notice warning %}}
If you get a `turtle.Terminator` error at any point, try closing the window with
the turtle and exiting the Python interpreter (<kbd>Ctrl</kbd>+<kbd>D</kbd>).
{{% /notice %}}

Before we get to writing functions, let's get to know our turtle. Open up an interactive console window and enter the following:

~~~text
>>> from turtle import *
~~~

Unlike using `import turtle`, this allows us to call the functions directly without prepending `turtle.` each time.

{{% notice warning %}}
Importing this way is very convenient but has its issues. For example, if you do
this in a file and define a function `forward`, you will no longer be able to
access the `forward` function from the turtle package.  We are using it now in
the interactive Python console because we're just going to be entering some
turtle commands to see how the turtle moves, i.e. not defining functions (yet!).
{{% /notice %}}

To get a window for your turtle to appear, you need to run any turtle functions. This is a good one to start:

~~~text
>>> clear()
~~~

Make sure you can type in the console and see the new turtle window at the same time. Now, try entering:

~~~text
>>> forward(200)
~~~

You should see the turtle dart forward (in the direction the arrow is facing) and leave a line behind it. Now try:

~~~text
>>> left(90)
~~~

You should see your turtle turn to the left by 90 degrees.

Try a few on your own! All the functions we can use are listed in [the docs](https://docs.python.org/3.3/library/turtle.html#turtle-methods) -- look specifically under "Move and draw" for some more to try. Make sure you click on the function before trying it to see what arguments it expects. If you can't get one that you want to try working, either call over a coach or just try using the ones listed above to move the turtle around a bit.

The Exercise
------------
***Problem 1*** Write the function `square` that draws a square with the side length as an argument.

Here's some code to get you started:

~~~text
def square(s):
	"""draws a square whose sides have length s
	"""
~~~

***Problem 2*** Write the function `initials` that draws your initials.

Here's some code to get you started:

~~~text
def initials():
	"""draws my initials: [your-initials-here]
	"""
~~~

***Problem 3*** Write the function `flower` that draws a flower using the `circle` function to draw petals.

Here is a basic `petal` function to start. Your `flower` function should call `petal()` to draw a single petal.

~~~text
def petal():
    """draws a petal
    """
    begin_fill()
    circle(100)
    end_fill()
~~~

A radius of `100` is just to give you a reasonable baseline -- change it to another size if you'd like! Also, using the `circle` function, the petals will overlap and look quite circular -- that's okay, we'll get to that soon!

{{% notice tip %}}
In addition to reading the docs about the `circle` function, try it out in the console like we did earlier! Remember to enter `from turtle import *` first, then try out some calls to `circle` with different values for the radius. The most important thing to take away is that the circle is drawn *to the left* of the turtle.
{{% /notice %}}

Here's some code to get your `flower` function started:

~~~text
def flower():
    """draws a flower
    """
    color('MediumSpringGreen')

    # draw your flower here using petal()
~~~

***Problem 4*** Modify your `flower` function to take a single argument: `flower_color`. This argument is a string that describes the color of the flower to be drawn by the function.

You can find a list of valid color names [here](https://www.tcl.tk/man/tcl8.4/TkCmd/colors.htm).

{{% notice info %}}
The three numbers next to each color name are what's called the RGB values associated with that color. You only need to give the `color` function the name, but those values can be used to preview the color if you go [here](https://www.rapidtables.com/web/color/RGB_Color.html) and input the corresponding values into the textboxes labeled "R", "G", and "B". You can otherwise just ignore these numbers and use your turtle to test out what the colors look like!
{{% /notice %}}

***Problem 5*** Modify the function `petal` to make the petals any shape you'd like! Once again, try using the Python interactive console to mess around with some ideas before writing any code in your file. Also feel free to change anything you'd like about the flower or petals!

{{% notice tip %}}
Each petal returns the turtle to exactly where it was when it started -- this is important! Otherwise, the petals won't be together in a flower!
{{% /notice %}}

