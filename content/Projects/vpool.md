---
title: "Vpool"
date: 2018-07-13T11:50:48-04:00
draft: true
---

![vpool](/images/vpool/pool.png)


Overview
--------

For this project, you will be writing a fully interactive 3D "pool-like" game using vPython. We say "pool-like" because the game need not satisfy the official rules of pool and the game may be substantially less complicated than a full pool game. In fact, "interesting" interpretations and wide variations in game play are welcome!

This project need not be pool, but should be a 3d interaction using vPython, with:

~~~text
- At least four gameplay objects (of some design).
- At least two kinds of implemented collisions, e.g., point-to-line and point-to-point collisions.
- Some kind of user control.
- A game objective!
- Include instructions---at least a text file on how to play the game
~~~

Documentation for  vPython
--------------------------

These are links are useful to have in one place:

- vPython documentation for each object, the scene, and other vPython features.
  - http://vpython.org/contents/doc.html   
- vPython examples 
  - http://www.glowscript.org/#/user/GlowScriptDemos/folder/Examples/ 


Don't start from scratch!

Instead, you can start from your vPython exercise code, and then make changes to those files to implement your game!

The reason for this is that you will absolutely want to run your code with every change you make, just to be sure it works. Don't write a large amount of code and then try to test it, there will be too many opportunities for things to go wrong; in the end, you'll need to remove it all and bring back each small change and test as you go!


***Examples to use...***

vPython offers this set of examples from which to start: http://www.glowscript.org/#/user/GlowScriptDemos/folder/Examples/

    The left-hand tab is GlowScript, which is our approach (the other tabs aren't useful for CS 5). 


In addition to Lab 12, here is a GlowScript gallery of example programs that show:

    Internal-wall collisions: An example that detects whether a sphere collides with the longest sides of a wall (or any length/width box).
    Two-sphere interaction: An example that checks for a collision between two spheres and changes their velocities realistically.
    Many-sphere interaction: An example that checks for a collision among many spheres and changes their velocities realistically.
    Random starting points: An example that shows how to randomly reposition an object (in this case, each time 'r' is pressed).


Requirements

This is, perhaps, the most open-ended of the final-project options. Even so, there are a number of requirements%G—%@but there is also plenty of freedom to personalize your game!

Here are the requirements (and a few "non-requirements") for your game:

    When the game is started, it should have a 3-dimensional "table" along with a collection of "pool balls." Your game can be very different than pool, but should have some staging area and some "actors" or "agents" within it. Just to standardize, we'll use "pool balls" for whatever characters you choose in your game.
    There should be a "cue ball," that is, some object that the player can strike or control directly, and at least 3 additional objects with which the cue ball can interact.
    Three should be "walls," or some other obstacles, delimiting the game field and through which game objects cannot pass. They should support "linear collisions," i.e., collisions with an object defined by a point and an extended object (a line or plane). A ball that hits a wall should use the "angle of incidence equals angle of reflection" rule.
    There should be some pockets in the table where the balls can fall%G—%@or some alternative notion of "goals" or "destination." Specifically, there should be some point-to-point interactions modeled and implemented, in addition to the point-to-line interactions mentioned above.
    To summarize the interactions needed, your program should handle point collisions and bounces in some way. That is, the different objects in the game should interact visibly during the game play. This is where your game should support at least some "spherical collisions," i.e., collisions between two objects defined by points. They don't need to be spheres, but they're welcome to be.
    Specifically, balls (characters) should not be able to pass through one another. It's nice to simulate the physics of ball-on-ball collisions using physical accuracy, but you may use other approximations or "wacky physics" for the spherical collisions. Just don't tell Profs. Gerbode and Esin that we used the words "wacky" and "physics" in the same sentence. Or feel free to let them know that it was one of the other CS profs who wrote this...
    However, your game should allow for multiple balls and objects moving "simultaneously". For example, if ball X hits ball Y then ball X presumably continues moving (in some direction) and ball Y begins moving. Both of these balls should be moving for a while. Moreover, ball X and ball Y may now hit other balls and these other balls may all need to move for some time as well. In other words, it is not acceptable for your program to always have at most one ball moving at a time.
    See the hint on how to compute collisions for several balls simultaneously below...
    You should have a well-defined game objective with clearly specified "win" conditions. It can be a one-person game, a two-person game, or a game against the computer opponent. That's totally up to you!
    Optional: It never hurts to have a "grutor" mode that makes the game easier to play or win (or a "professor" mode in which you win immediately!).
    Your program should somehow alert the user when they have won the game!
    Your program must have an easy-to-use vPython interface (some combination of mouse and keyboard) that allows the user to hit the "cue ball" in different directions (optionally, with varying velocity). You do not need to have an actual "cue stick," but you're certainly welcome to do so. There are lots of other ways to handle the interface and this is entirely up to you.
    Your milestone and final project documentation should include a plain-text milestone.txt or final.txt file that describes the objective of your game and how to use the user interface. If you want, a short summary of the controls can also appear in the game itself. 

And, of course, feel free to add additional features as you wish!


Handling friction...

    Warning Sometimes, vPool authors model friction by multiplying velocities by a constant less than 1 each time step. Note that the velocities never get to zero this way! It can be frustrating if it takes a very long time for objects to come to rest%G—%@before making another shot, for example. One way to avoid frustrating yourself (and the CS 5 graders!) is to check for slowly-moving objects and then simply set their velocities to 0. Once all velocities are zero, the next "move" in the game can be made. 

Here are a few tips that may be helpful to you:

    First, remember that the vPython reference page is a self-contained resource for vPython.
    This vPython_events.py file is an example of one way to manage motion, keypresses, and mouse events. (NOTE: this code won't run on GlowScript, but it still has some useful ideas.
    The vPython arrow object can be used instead of drawing a pool cue to indicate the direction in which you will strike the cue ball. For example, the user might use the mouse or keyboard to rotate an arrow centered at the cue ball. Then another user input, such as hitting the space bar, could be used to cause the cue ball to move.
    See the vPython reference page for information on how to get keyboard and mouse input from the user...
    Using a vector to keep track of the direction of movement of a ball allows for easy animation. Moreover, if the ball collides with another object then you need only update the vector appropriately. 


Notes and hints

How do I handle all the collisions for lots of different objects?!

It may seem like you would need a zillion conditional statements to handle collisions for many objects, but you don't have to do all of them separately!

What many people do in this situation is to first create their objects:

ball1 = sphere(...stuff..)
ball2 = sphere(...stuff..)
ball3 = sphere(...stuff..)
ball4 = sphere(...stuff..)
...

and then make a list: L = [ball1, ball2, ball3, ball4, ...]

and then, to compute collisions, they run two loops through the list. Note that we only check each pair once here!

for i in range(len(L)):
  for j in range(i + 1, len(L)): # note we start at i + 1
     if  collide(L[i], L[j]) == True:
        # do something appropriate...

That way you can write a single function (collide) to check if two balls collide, and then use it for all pairs...

If you want the code for realistic "elastic" physical collisions, see this page: VPythonCollisionExample


What to Submit for the Milestone and Final Project

For the milestone and final submissions, you should submit a version for which the following pieces are implemented and work:

    A text document called milestone.txt or, for the final project, final.txt, with your name and the name of your partner (if any), the project that you've chosen, and a brief description of your plans for your game. One paragraph will suffice for the description. Also, include a description of the objective of the game%G—%@and how we should run it!
    In addition, your final.txt document should give instructions for playing the game as it currently operates, e.g. "Pressing the "s" key will do one thing, the mouse will allow the user to do another thing, etc."
    [For the milestone]    Implementation of enough of the functions, with docstrings, that the game does something interesting (even if it is far short of the complete implementation) in a file called milestone.py.
    Specifically, your program should include at least some "linear" collisions (a point object with a plane or a line) and at least some "spherical" collisions (a point object with another point object).
    Include any other files needed to test your game, as well. All of these should be zipped into vpython_milestone.zip for the milestone or vpython_final.zip for the final version, and then submitted.
    [For the final]    You should submit a single final.zip file that includes the following:
        A text document called final.txt that provides a description of the game and its objectives and complete instructions for how to play the game.
        Your full game in a file called final.py.
        Be sure to include any other files needed to play your game, e.g., sounds, other Python files that get imported, etc. 

