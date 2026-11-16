---
title: "Mutation Madness"
date: 2018-07-04T09:53:38-04:00
draft: false 
weight: 2200
---

 In this section you will write several functions that modify a list. Unlike previously when you worked with lists, these function will not return anything. Instead they will modify the entries in the list passed in. You may not use the built-in `python` functions `reverse` or `remove` in your solutions.

**Problem 1**: `threshold( L, thresh )`
    This function takes a list of numbers, `L`, and a minimum value, `thresh`, and modifies that array such that any element in the array that is not above the minimum value is zeroed. 


**Problem 2**: `my_reverse(L)`
    This function reverses a list in place. That is, it does not create a copy of the list, even during the reversal process (i.e., it's not OK to create a copy, read in the elements backwards and then copy those elements back to the original array). You may not use `python`'s builtin `reverse()` function for this problem. 


**Problem 3**: `smooth(L)`
    In many domains, it is advantageous to smooth data before processing it. Smoothing is accomplished by aggregating the data in one location with data nearby. Write a method that smooths the data in an array by replacing it with the average value of it and its immediate neighbors. Be careful to average the original values, not the new values. However, your function should ultimately modify the array it was passed, rather than returning a copy of the array. Before you write your function, think through your algorithm. You may find it useful to draw pictures. 


**Problem 4**: `my_remove( L, e )`
    This function removes all instances of the specified element `e` from the list L. If `e` is not in `L`, `L` remains unchanged. 

