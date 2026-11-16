---
title: "Building a Date Class"
date: 2018-07-09T09:30:49-04:00
weight: 2500
---

In this exercise, we'll be creating our own datatype: a class called `Date`.

The `Date` Class
----------------

Here is some starter code for the `Date` class.

~~~text
class Date(object):
    """ a user-defined data structure that
        stores and manipulates dates
    """

    def __init__(self, month, day, year):
        """ the constructor for objects of type Date """
        self.month = month
        self.day = day
        self.year = year


    def __repr__(self):
        """ This method returns a string representation for the
            object of type Date that calls it (named self).

             ** Note that this _can_ be called explicitly, but
                it more often is used implicitly via the print
                statement or simply by expressing self's value.
        """
        s = "%02d/%02d/%04d" % (self.month, self.day, self.year)
        return s


    def isLeapYear(self):
        """ Returns True if the calling object is
            in a leap year; False otherwise.
		"""
        if self.year % 400 == 0:
            return True
        elif self.year % 100 == 0:
            return False
        elif self.year % 4 == 0:
            return True
        else:
            return False
~~~

The `Date` class has three attributes:

 - `year` to hold the year
 - `month` to hold the month of the year
 - `day` to hold the day of the month

{{% notice note %}}
The parameters `year`, `month`, and `day` are different than the attributes `year`, `month`, and `day`. The parameters are variables whose values are only accessible from the `__init__` method during the creation of a `Date` object while code in `__init__` is being executed. On the other hand, the attributes are bound to specific `Date` objects and can be accessed as long as the object still exists by prepending `self.`.
{{% /notice %}}

The `Date` class has three methods:

 - `__init__` is the *constructor*. A constructor is a method that contains code that gets executed for new `Date` objects as they are created.
 - `__repr__` is a method that gets called when a `Date` object is used in a print statement or any string context. When you call `print(d)` for some `Date` object `d`, the `__repr__` method is called to generate the string that gets printed.
 - `isLeapYear` is a user-defined method that returns whether a `Date` object's
   associated year is a leap year.

Methods
-------

Traditionally, functions called by objects are called *methods*. Methods are just special functions that are defined with respect to a class and get called by specific objects of that class. For example:

~~~text
>>> d = Date(11, 10, 2009) # create a `Date` object
>>> d.isLeapYear()         # call the `isLeapYear` method on `d`
False

>>> d2 = Date(3, 15, 2008) # create a different `Date` object
>>> d2.isLeapYear()        # calling the same method on a different object
True
~~~

Even without passing any parameters as input to a method, methods have access to any data associated with the object they're called on. You can see in `isLeapYear` that `self.year` is used to access the `year` attribute of *whichever `Date` object calls it*.

Self
----
In the above example, a method defined once in the `Date` class is called twice --- on different `Date` objects. In a method definition (where the function is defined in the class), the `self` keyword is used to refer to the object that called the method.

{{% notice note %}}
If you take a look at the methods in the `Date` class starter code, you'll see that the first parameter in all of them is `self`. Methods in Python always take `self` as their first parameter. Even in the case of `isLeapYear` where there are no parameters passed when it's called, it still has the `self` parameter because it is a method.
{{% /notice %}}

Getting Started
---------------

Let's mess around with our `Date` class to get familiar:

~~~text
# create a Date object
>>> d = Date(11, 10, 2009)

# show d's value (this uses __repr__)
>>> d
11/10/2009

# print d's value (also uses __repr__)
>>> print('Tuesday is', d)
Tuesday is 11/10/2009

# create another object named d2
>>> d2 = Date(11, 10, 2009)

# show d2's value
>>> d2
11/10/2009

# are they the same?
>>> d == d2
False

# yet another object of type Date
>>> d3 = Date(1, 1, 2012)

# check if d3 is in a leap year
>>> d3.isLeapYear()
True

# check if d2 is in a leap year
>>> d2.isLeapYear()
False
~~~

More Methods
------------

Now, let's add two methods to our `Date` class: `copy` and `equals`.

***Copy***

~~~text
def copy(self):
    """ Returns a new object with the same month, day, year
        as the calling object (self).
    """
    d = Date(self.month, self.day, self.year)
    return d
~~~

Make sure this goes inside your `Date` class!

The `copy` method returns a newly constructed `Date` object with the same associated year, month, and day as the `Date` object being copied. We can check this by look at memory addresses with the `id` function.

~~~text
>>> d = Date(1, 1, 2010) # create a Date object
>>> d2 = d.copy()        # create another Date object with the same date as d

>>> d
01/01/2010
>>> d2
01/01/2010

>>> id(d)
430568
>>> id(d2)
413488

>>> d == d2
False
~~~

You can see that both `d` and `d2` hold the same date but are two distinct `Date` objects stored in different places.

***Equals***

~~~text
def equals(self, d2):
    """ Decides if self and d2 represent the same calendar date,
        whether or not they are the in the same place in memory.
    """
    return self.year == d2.year and self.month == d2.month and self.day == d2.day
~~~

The `equals` method returns `True` if the calling object (named `self`) and the input object (named `d2`) represent the same calendar date, otherwise `False`. That is to say, the year, month, and day attributes for each object are equal.

~~~text
>>> d = Date(1, 1, 2010)
>>> d2 = d.copy()

>>> d
01/01/2010
>>> d2
01/01/2010

>>> d == d2 # still not the same object
False

>>> d.equals(d2) # but they hold the same date
True
~~~

Exercises
---------

***Problem 1*** Write the `tomorrow` method for `Date`.

~~~text
def tomorrow(self):
~~~

`tomorrow` should not return anything. Rather, it should change the date stored in the calling object so that it represents the next day.

~~~text
>>> d = Date(12, 31, 2009)
>>> d
12/31/2009

>>> d.tomorrow()
>>> d
01/01/2010

>>> d2 = Date(2, 28, 2012)
>>> d2
02/28/2012

>>> d2.tomorrow()
>>> d2
02/29/2012

>>> d2.tomorrow()
>>> d2
03/01/2012
~~~

***Problem 2*** Write the `yesterday` method for `Date`.

~~~text
def yesterday(self):
~~~

`yesterday` should not return anything. Rather, it should change the date stored in the calling object so that it represents the previous day.

~~~text
>>> d = Date(1, 1, 2010)
>>> d
1/1/2010

>>> d.yesterday()
>>> d
12/31/2009

>>> d2 = Date(3, 1, 2012)
>>> d2
03/01/2012

>>> d2.yesterday()
>>> d2
02/29/2012

>>> d2.yesterday()
>>> d2
02/28/2012
~~~

***Problem 3*** Write the `addNDays` method for `Date`.

~~~text
def addNDays(self, N):
~~~

`addNDays` takes one argument as input (`N`, a nonnegative integer). It should not return anything. Rather, it should change the calling object so that it represents `N` calendar days following the original date.

{{% notice tip %}}
How might you use `tomorrow` to implement this?
{{% /notice %}}

`addNDays` should also *print* (including the original and new date) each date between the original and new date. Remember that we can print `Date`s just by passing a `Date` object to print.

~~~text
>>> d = Date(11, 10, 2009)
>>> d
11/10/2009

>>> d.addNDays(3)
11/10/2009
11/11/2009
11/12/2009
11/13/2009

>>> d
11/13/2009

>>> d2 = Date(11, 27, 2007)
>>> d2
11/27/2007

>>> d2.addNDays(1265)
11/27/2007
11/28/2007

... lots of dates skipped ...

05/14/2011
05/15/2011

>>> d2
5/15/2011
~~~

You can make your own tests [here](https://www.timeanddate.com/date/dateadd.html).

***Problem 4*** Write the `subNDays` method for `Date`.

~~~text
def subNDays(self, N):
~~~

`subNDays` takes one argyment (`N`, a nonnegative integer). It should not return anything. Rather, it should change the calling object so that it represents `N` calendar days before the original date.

{{% notice tip %}}
How might you use `yesterday` to implement this?
{{% /notice %}}

`subNDays` should also *print* (including the original and new date) each date between the original and new date. Remember that we can print `Date`s just by passing a `Date` object to print.

For testing, try reversing the cases used for testing `addNDays`.

***Problem 5*** Write the `isBefore` method for `Date`.

~~~text
def isBefore(self, d2):
~~~

`isBefore` takes one argument (`d2`, a `Date` object) and returns `True` if the date associated with the calling object occurs before the date associated with `d2`. Otherwise, it returns `False`.

~~~text
>>> d = Date(11, 11, 2009)
>>> d2 = Date(1, 1, 2010)

>>> d.isBefore(d2)
True
>>> d2.isBefore(d)
False
>>> d.isBefore(d)
False
~~~

***Problem 6*** Write the `isAfter` method for `Date`.

~~~text
def isAfter(self, d2):
~~~

`isAfter` takes one argument (`d2`, a `Date` object) and returns `True` if the date associated with the calling object occurs after the date associated with `d2`. Otherwise, it returns `False`.

For testing, try reversing the cases used for testing `isBefore`.

***Problem 7*** Write the `diff` method for `Date`.

~~~text
def diff(self, d2):
~~~

`diff` takes one argument (`d2`, a `Date` object) and returns an integer representing the number of days between the calling object and `d2`.

Unlike previous methods implemented thusfar, `diff` should NOT change the calling object or `d2`. If you want to manipulate one of them, you'll have to make a copy first. The sign of the returned integer is important: negative when `self` is before `d2` and positive when `self` is after `d2`.

{{% notice tip %}}
Don't try and count years and months between the dates --- just stick to days. On that same note, don't use `addNDays` or `subNDays` either. Using `addNDays` or `subNDays` amounts to checking every possible difference between two days, which is too slow.
{{% /notice %}}

~~~text
>>> d = Date(11, 10, 2009)
>>> d2 = Date(12, 18, 2009)

>>> d2.diff(d)
38
>>> d.diff(d2)
-38

>>> d # make sure they don't change!
11/10/2009
>>> d2
12/18/2009

>>> d3 = Date(5, 15, 2013)
>>> d3.diff(d)
1282
~~~

***Problem 8*** Write the `dow` method for `Date`.

~~~text
def dow(self):
~~~

`dow` takes no arguments and returns a string representing the day of the week of the date associated with the calling `Date` object.

{{% notice tip %}}
How might it help to find the diff from a *known* date, like Tuesday, November 11, 2008? How might the mod operator ( `%` ) help?
{{% /notice %}}

~~~text
>>> d = Date(12, 7, 1941)
>>> d.dow()
'Sunday'

>>> Date(10, 28, 1929).dow()
'Monday'

>>> Date(10, 19, 1987).dow()
'Monday'

>>> d = Date(1, 1, 2100)
>>> d.dow()
'Friday'
~~~

Extra Bonus Challenge
---------------------

Write the `nyCounter` function. This is *not* a method so should not be defined in the `Date` class. However, it does *use* the `Date` class!

`nyCounter` takes two arguments (`start` and `stop`, both integers representing years) and prints how often New Year's Day occurs on each day of the week.

~~~text
>>> nyCounter(2000, 2009)
Monday    = 2
Tuesday   = 2
Wednesday = 1
Thursday  = 2
Friday    = 0
Saturday  = 2
Sunday    = 1
~~~

