---
title: "Exact Change"
date: 2018-06-29T10:14:07-04:00
draft: false
weight: 1580
---

Objectives
----------
 - Practice, practice, practice!

***Problem*** Write the `exact_change` recursive function.

`exact_change` takes two argumens (`target_amount` and `L`) where `target_amount` is a non-negative integer (i.e. >= 0) and `L` is a list of positive integers (i.e. > 0). The `exact_change` function should return `True` if it is possible to create `target_amount` by adding up some or all of the values in `L`. Otherwise, if it is not possible, it should return `False`.

You can think of `L` as representing the values of coins in your pocket. `exact_change` then answers the question of whether you can pay for an item that costs `target_amount` *exactly*.

Here is some example output:

~~~text
>>> exact_change(42, [25, 1, 25, 10, 5, 1])
True

>>> exact_change(42, [25, 1, 25, 10, 5])
False

>>> exact_change(42, [23, 1, 23, 100])
False

>>> exact_change(42, [23, 17, 2, 100])
True

>>> exact_change(42, [25, 16, 2, 15])
True  # needs to be able to "skip" the 16...

>>> exact_change(0, [4, 5, 6])
True

>>> exact_change(-47, [4, 5, 6])
False

>>> exact_change(0, [])
True

>>> exact_change(42, [])
False
~~~

{{% notice tip %}}
You can use *branching recursion* for this problem. All that means is that you'll have more than 1 recursive function call (like when you drew the Koch snowflake with turtles!). For some `L`, we can try solving `exact_change` either with or without the first value. Remember this varying exclusion of the first value will occur at every recursive call, so as you augment `L` before passing it to the next recursive call, what "the first value" references will change. Once every recursive call is passed a different combination of values from `L`, all that's left is to add the logic that determines whether we've solved the problem that `exact_change` is trying to solve.
{{% /notice %}}
