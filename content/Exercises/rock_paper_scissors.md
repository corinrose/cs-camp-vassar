---
title: "Rock, Paper, Scissors"
date: 2018-06-14T10:04:14-04:00
weight: 800
---

Objectives
----------
- Practice creating new Python files (in this case, by copying old ones or starting with the code below)
- Learn to write a bit of your own code (by altering our starter program, if you wish)
- Get comfortable with text-based input and output in Python 

Background
----------
Start by creating a new file called something unique, such as `rock_paper_scissors.py`, in vscode.

You should also create a new folder for this file in your `cscamp` folder---whatever you called it.

Remember that we can create and edit a file with the command `code rock_paper_scissors.py`---recall this will create and edit the file in your current working directory.

At this point, your directory for this class could look something like this
~~~text
$ tree cscamp
cscamp
├── fours
│   └── fours.py
├── picobot
│   ├── empty_6rules.txt
│   └── maze_12rules.txt
└── rock_paper_scissors
    └── rock_paper_scissors.py
~~~

Of course, you are welcome to name your folders and files whatever you like, but make sure you are organizing your files somehow or it will become a huge pain later in the class! You can look at your directory structure with the `tree` command, as above.

{{% notice note %}}
Remember to be sure to type the `.py` extension: it enables syntax highlighting, i.e., code colorization.
{{% /notice %}} 

Now you can paste the following code into this file and save: 
~~~text
# Vassar CS Camp 
# Name: [your name here]
# Filename: rock_paper_scissors.py

import random          # imports the library named random

user = input("Choose your weapon: ")
comp = random.choice(['rock','paper','scissors'])
print()

print('The user (you)   chose', user)
print('The computer (I) chose', comp)
print()

if user == 'rock':
    print('Ha! I really chose paper--I WIN!')

print("Better luck next time...")
~~~

**How do we run this file?**

First, make sure you are in the same directory as the file---you can do so by checking if the file is in your current directory with `ls`:
~~~text
$ ls
rock_paper_scissors.py
~~~

While in the same folder as the `.py` file, we can run the file simply by passing it's name into the `python` command
~~~text
$ python rock_paper_scissors.py
...
~~~ 

We can of course edit the file with vscode from the command line
~~~text
$ code rock_paper_scissors.py
~~~

The Exercise
------------

Use the discussion from class and the starter code (above) to create a program that:

- Invites the user to play a game of "rock-paper-scissors."
- Lets the user choose from at least three options
  - They don't have to be rock, paper, and scissors---feel free to vary the actors!
  - But your program does have to work differently for each of three distinct inputs (well, at least three inputs) 
- Your program is welcome to play an honest game of RPS, but you're also welcome to create a player that always wins (or, if you prefer, that always loses) 
- Your program should echo the choice the user made
- You may assume the user will type her/his choice correctly, for your game's choices... 
- Your program should reveal the choice that it makes (whether fair or not)
- Your program should print out who won that round (or whether it was a tie, or some other outcome)
- Adding comments explaining how your code works is strongly encouraged! 

In brief, the program should ask the user to choose rock, paper, or scissors (or your own variants!). Then it should repeat that choice back to the user, reveal its own choice, and finally report the results. The program can play fairly, can always win, or can always lose---it's up to you. If RPS is unfamiliar, in the game of [rock-paper-scissors](http://worldrps.com/), rock defeats scissors, scissors defeat paper, and paper defeats rock. 

Don't hesitate to get creative with the dialogue and the choice of 'weapon!'


Optional bonus challenge
------------------------
Too much time on your hands? Add "lizard" and "spock" as noted at this [RPSSL](http://www.samkass.com/theories/RPSSL.html) link.

<!-- > - Even more time? Consider [RPS-25](http://www.umop.com/rps25.htm), a strict superset of RPS.
> - But if you have enough time for [RPS-101](http://www.umop.com/rps101.htm), there's a problem! 
> 
> Want your program to continue playing many times? Use a `while True:` loop.
> 
> We'll provide two examples instead of detailed explanations:
~~~text
while True:
  print("Still running...")
  response = input("Play again? ")
  if response == 'n':
    break
~~~
>
> Here is another possibility:
>
~~~text
running = True
while running:
  response = input("Play again? ")
  if response == 'n':
    running = False
~~~
> Feel free to ask one of the coaches about this. 
> -->

When you're done
----------------
When you finish this exercise, raise your hand to call over a coach. We'll come by and go through your solution with you!
