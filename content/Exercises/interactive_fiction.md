---
title: "Interactive Fiction"
date: 2018-06-14T10:34:10-04:00
weight: 900
---

Objectives
----------
- Get comfortable working with code branching using `if`, `elif`, and `else`.
- Begin working in larger and more complex `python` files.

Background
----------

For this problem, you---the author--should create a Python program (built on the starting template below) that is a work of interactive fiction, a.k.a., a choose-your-own-adventure program. It needs to include at least 5 if-based control structures, as noted below: 

**An example from which to build**

Start by creating a file, we will call it `fiction.py`, and pasting this skeleton of a story into it:

~~~text
# Vassar CS Camp
# Name: [your name here]
# Filename: fiction.py

""" 
Title for your adventure:   The Quest.

Notes on how to "win" or "lose" this adventure:
  To win, choose the table.
  To lose, choose the door.

"""

import time

""" this function runs one session of interactive fiction
    Well, it's "fiction," depending on the pill color chosen...
    arguments: no arguments (prompted text doesn't count as an argument)
    results: no results     (printing doesn't count as a result)
"""
delay = 0.0          # change to 0.0 for testing or speed runs,
                     # ..larger for dramatic effect!

username = input("What do they call you, worthy adventurer? ")

print()
print("Welcome,", username, " to the Libra Complex, a labyrinth")
print("of weighty wonders and unreal quantities...of poptarts!")
print()

print("Your quest: To find--and partake of--a poptart!")
print()
flavor = input("What flavor do you seek? ")
if flavor == "strawberry":
    print("Wise! You show deep poptart experience.")
elif flavor == "s'mores":
    print("The taste of the campfire: well chosen, adventurer!")
else:
    print("Each to their own, then.")
print()

print("On to the quest!\n\n")
print("A corridor stretches before you; its dim lighting betrays, to one side,")
print("a table supporting nameless forms of inorganic bulk and, to the other,")
print("a door ajar, leaking laughter--is that laughter?--of lab-goers.")
time.sleep(delay)
print()

choice1 = input("Do you choose the table or the door? [table/door] ")
print()

if choice1 == "table":
    print("As you approach the table, its hazy burdens loom ever larger, until...")
    time.sleep(delay)
    print("...they resolve into unending stacks of poptarts, foil shimmering.")
    print("You succeed, sumptuously, in sating the challenge--and your hunger.")
    print("Go well,", username, "!")

else:  
    print("You push the door into a gathering of sagefowl, athenas, and stags alike,")
    print("all relishing their tasks. Teamwork and merriment abound here, except...")
    time.sleep(delay)
    print("...they have consumed ALL of the poptarts! Drifts of wrappers coat the floor.")
    print("Dizzy, you grasp for a pastry. None is at hand. You exhale and slip")
    print("under the teeming tide of foil as it finishes winding around you.")
    print("Farewell,", username, ".")
~~~

Try out the above story by

- Opening the integrated terminal in vscode
- `cd` to the directory where `fiction.py` is located
- Running `python fiction.py`

Once you've done that, try it *at least twice* to show the different paths through the story.

> The Exercise
> ------------
>
> You're ready to go! Partner up with someone, if you'd like (entirely optional!) and create your own adventure.
> 
> Certainly feel free to modify or continue the poptart-related story---or, if you wish, do something completely different to compose your own work of interactive fiction. The story above includes two `if`-based control structures: (a) an `if-elif-else` and (b) an `if-else`.
> 
> The requirement of this problem is that you use each of five *conditional control structures* in a way that affects the story or dialog. They don't have to appear in this order, and you're welcome to have many more than this if you wish! 
> 
> Here are the control structures to be sure to include:
> 
> 1. An `if`, `elif`, and `else` control structure (with exactly one `elif`)
> 2. An `if`, `elif`, `elif`, ... and `else` control structure (with at least two `elif`s)
> 3. An `if`, `else` control structure (with zero `elifs`)
> 4. An `if`, `elif`, ... control structure (with one or more `elifs` but no trailing `else` at all)
> 5. An `if` control structure (with no trailing `elif` nor trailing `else` at all) 
> 
> Please keep things light! There are forums for all forms of expression---this one's for contextualizing conditionals in CS.
> 
> So, keep in mind that, potentially, lots of people (our coaches!) will read---and run---your story (we look forward to it!) Also, please be mindful of the time you spend! The goal here is not to take a lot of time. (It's easy to let time slip away: the poptart adventure above took much longer than I originally thought it would---and it has only *one* control structure!) 

When you're done
---------------------
When you finish this exercise, raise your hand to call over a coach *if* you would like someone to go through your solution with you!
