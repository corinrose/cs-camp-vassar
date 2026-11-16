---
title: "TT Securities, Incorporated"
date: 2018-07-04T09:27:54-04:00
draft: false
weight: 2100
---

Background
----------

{{% notice note%}}
For this exercise, do not use the built-in functions `sum`, `min`, or `max` here---instead, as you work through the different menu options, write helper functions that handle the data appropriately. 
{{% /notice %}}

**Starter code**

In class, we looked at an example user-interaction loop. Here is a variation on that code---this may be a good place to start with this problem. We've named the primary function `main()` in order to set things up similar to how you'll write the larger version described below:

~~~text
#
# Example user-interaction looping program
#  (a variant of the one done in class)
#

def menu():
    """A function that simply prints the menu"""
    print()
    print("(0) Continue!")
    print("(1) Enter a new list")
    print("(2) Predict the next element")
    print("(9) Break! (quit)")
    print()

def predict(L):
    """Predict ignores its argument and returns
       what the next element should have been.
    """
    return 42

def find_min(L):
    """find min uses a loop to return the minimum of L.
       Argument L: a nonempty list of numbers.
       Return value: the smallest value in L.
    """
    result = L[0]
    for x in L:
        if x < result:
            result = x
    return result

def find_min_loc(L):
    """find min loc uses a loop to return the minimum of L
            and the location (index or day) of that minimum.
        Argument L: a nonempty list of numbers.
        Results:  the smallest value in L, its location (index)
    """
    minval = L[0]
    minloc = 0

    for i in list(range(len(L))):
        if L[i] < minval:  # a smaller one was found!
            minval = L[i]
            minloc = i

    return minval, minloc

def main():
    """The main user-interaction loop"""

    L = [30, 10, 20]  # an initial list

    while True:     # the user-interaction loop
        print("\n\nThe list is", L)
        menu()
        choice = input("Choose an option: ")

        #
        # "Clean and check" the user's input
        # 
        try:
            choice = int(choice)   # make into an int!
        except:
            print("I didn't understand your input! Continuing...")
            continue

        # run the appropriate menu option
        #
        if choice == 9:    # We want to quit
            break          # Leaves the while loop altogether

        elif choice == 0:  # We want to continue...
            continue       # Goes back to the top of the while loop

        elif choice == 1:  # We want to enter a new list
            newL = input("Enter a new list: ")    # enter _something_
            #
            # "Clean and check" the user's input
            #
            try:
                newL = str.split(newL, ",")   # split is a function in the str package
                if type(newL) != type([]):
                    print("That didn't seem like a list. Not changing L.")
                else:
                    # Convert elements of the list from strings to ints
                    fList = []
                    for ele in newL:
                        fList += [int(ele)]
                    L = fList  # Here, things were OK, so let's set our list, L
            except:
                print("I didn't understand your input. Not changing L.")

        elif choice == 2:  # Predict and add the next element
            n = predict(L) # Get the next element from the predict function
            print("The next element is", n)
            print("Adding it to your list...")
            L = L + [n]    # ...and add it to the list

        elif choice == 3:  # Unannounced menu option!
            pass       # this is the "nop" (do-nothing) statement in Python

        elif choice == 4:  # Unannounced menu option (slightly more interesting...)
            m = find_min(L)
            print("The minimum value in L is", m)

        elif choice == 5:  # Another unannounced menu option (even more interesting...)
            minval, minloc = find_min_loc(L)
            print("The minimum value in L is", minval, "at day #", minloc)

        else:
            print(choice, " ?      That's not on the menu!")

    print()
    print("See you yesterday!")

main()
~~~

The TTS Problem
---------------

For this problem, you will implement a (text-based) menu of options for analyzing a list of stock prices (or any list of floating-point values). This provides an opportunity to use loops in a variety of ways, as well as experience handling user input.

The top-level function to write for this problem is called `main()`. Note that it takes no arguments. Instead, it should offer the user a menu with these choices:

~~~text
(0) Input a new list
(1) Print the current list
(2) Find the average price
(3) Find the minimum and its day
(4) Find the maximum and its day
(5) Your TT investment plan
(9) Quit

Enter your choice:
~~~

Feel free to change the wording or text, but please keep the functionality of these choices intact. If you'd like to add additional menu options of your own design, please use different values for them.

Once the menu is presented, the program should wait for the user's input. (You may assume that the user will type an integer as input.) The function should then

- Print a warning message if the integer is not a valid menu option
- Quit if the user inputs `9`
- Allow the user to input a new list of stock prices, if the user selects choice `0`
- Print a table of days and prices, with labels, if the user selects choice `1`
 - Compute the appropriate statistics about the list for choices `2`-`5`

For any option except `9`, the function should reprompt the user with the menu after each choice.

**formatting neatly...**

This is ***optional***, but if you'd like to print neatly-formatted columns, the following approach will help. Try pasting the examples at the `python` prompt, just to get the hang of it). The formatting-string indicates how things are formatted, and the inputs to `.format` pass what values will get formatted that way.

~~~text
>>> print("{0: >4} : $ {1: >6}".format("Day", "Price"))
 Day : $  Price

>>> print("{0: >4} : $ {1: >6}".format(3, 42))
   3 : $     42

>>> print("{0: >4} : $ {1: >6}".format(11, 27042))
  11 : $  27042
~~~

Briefly, the formatting string, namely `"{0: >4} : $ {1: >6}"` is saying three things:

- Print the format-argument #0 right-justified in a space with a width of 4
- Then, print a space, a colon, a space, a dollar sign, and a space (all exactly as shown)
- Then, print the format-argument #1 right-justified in a space with a width of 6

Notice that the `.format(input0, input1)` after the formatting string provides the values needed!

Experiment with this to get it to look the way you'd like. And printing without worrying about the format is totally fine, too! 

**The time-travel strategy**

 For menu option 5, you will want to find the best day on which to buy and sell the stock in question in order to maximize the profit earned. However, the sell day must be greater than or equal to the buy day. You may want to adapt the example function `diff` from class to find this maximum profit.

**Helper functions**

You need to write a helper function for each of the menu options 2-5. (The others already work or don't need an additional function.)

Also, especially for option 5, note that you can always return more than one value from a function. For example,
~~~text
def f(x):
    return x, (x+4)
~~~
This function can be called as follows:
~~~text
a, b = f(38)
~~~
In this case, `a` will receive the value `38` and `b` will receive `42`.

Another way to return multiple values from a function is to return a list.  Either approach is fine. 

Here is an example run---you do not need to follow this format exactly (though you may), but it's meant to show an example of each menu possibility:

~~~text
>>>  main()
(0) Input a new list
(1) Print the current list
(2) Find the average price
(3) Find the standard deviation
(4) Find the min and its day
(5) Find the max and its day
(6) Your TT investment plan
(9) Quit

Enter your choice: 0
Enter a new list of prices: [20, 10, 30]
(0) Input a new list
(1) Print the current list
(2) Find the average price
(3) Find the standard deviation
(4) Find the min and its day
(5) Find the max and its day
(6) Your TT investment plan
(9) Quit

Enter your choice: 1

Day  Price
---  -----
  0  20.00
  1  10.00
  2  30.00


(0) Input a new list
(1) Print the current list
(2) Find the average price
(3) Find the standard deviation
(4) Find the min and its day
(5) Find the max and its day
(6) Your TT investment plan
(9) Quit

Enter your choice: 2

The average price is 20.0


(0) Input a new list
(1) Print the current list
(2) Find the average price
(3) Find the standard deviation
(4) Find the min and its day
(5) Find the max and its day
(6) Your TT investment plan
(9) Quit

Enter your choice: 3

The st. deviation is 8.16496580928


(0) Input a new list
(1) Print the current list
(2) Find the average price
(3) Find the standard deviation
(4) Find the min and its day
(5) Find the max and its day
(6) Your TT investment plan
(9) Quit

Enter your choice: 4

The min is 10 on day 1


(0) Input a new list
(1) Print the current list
(2) Find the average price
(3) Find the standard deviation
(4) Find the min and its day
(5) Find the max and its day
(6) Your TT investment plan
(9) Quit

Enter your choice: 5

The max is 30 on day 2


(0) Input a new list
(1) Print the current list
(2) Find the average price
(3) Find the standard deviation
(4) Find the min and its day
(5) Find the max and its day
(6) Your TT investment plan
(9) Quit

Enter your choice: 6
Your TTS investment strategy is to

  Buy on day 1  at price 10
 Sell on day 2  at price 30

 For a total profit of 20


(0) Input a new list
(1) Print the current list
(2) Find the average price
(3) Find the standard deviation
(4) Find the min and its day
(5) Find the max and its day
(6) Your TT investment plan
(9) Quit

Enter your choice: 7


The choice 7 is not an option.
Try again



(0) Input a new list
(1) Print the current list
(2) Find the average price
(3) Find the standard deviation
(4) Find the min and its day
(5) Find the max and its day
(6) Your TT investment plan
(9) Quit

Enter your choice: 9
~~~

If you'd like, you may add other menu options (under different numeric labels) that process the list in some other way of your design---it can be serious or not.
