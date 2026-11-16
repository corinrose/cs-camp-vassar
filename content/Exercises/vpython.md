---
title: "VPython"
date: 2018-07-11T10:31:42-04:00
draft: false
weight: 2800
---

Background
----------

This exercise invites you to explore a variant of `python`, called `vpython`, which is:

- *Object-oriented* (everything is organized via objects and classes),
- *Web-based* (everything runs in your browser), and
- *Graphical* (you'll build and program the behavior of 3D models). 

The goal of this lab is to explore `vpython` in order to understand---and extend---a 3D interaction. If you enjoy working with `vpython`, you might consider a `vpython`-based final project in the upcoming weeks, as well. In that final project, the goal could be to create a game or interaction of your own design. 

Documentation
-------------

These links may be useful to have in one place:

- Documentation for each object, the scene, and other `vpython` features.
    - http://vpython.org/contents/doc.html 
- `vpython` examples:
    - http://www.glowscript.org/#/user/GlowScriptDemos/folder/Examples/
    - http://vpython.org/contents/contributed.html
    
Remember that these links are here, but for now let's begin with an example... 

Getting Started
---------------

~~~text
from vpython import *

# The simplest possible vpython program:
box(color = vector(1.0, 1.0, 1.0))

# Try changing the color: the components are
#   red, green, blue    each from 0.0 to 1.0

# Then, add a second parameter:   size = vector(2.0, 1.0, 0.1)
#       The order of those three numbers: Length, Height, Width

# Then, a third parameter:  axis = vector(2, 5, 1)
#       The order of those three numbers: x, y, z
~~~

Then, run it. It may pause for a second, but should eventually open up a web browser with a 3D box! Make sure you can

- Rotate the cube (right mouse button)
- Zoom in and out from the cube (scroll wheel or two-finger drag) 

***Task 1: Play around with the three components of the color...***

- They're in (red, green, blue) order
- They're between `0.0` and `1.0`
- They need to be specified as a vector (note the `vector(r, g, b)` constructor: in `python`, everything is an object...) 

***Task 2: Play around with the three components of the size...***

Grab the size parameter and place it (after a comma) into the creation of the box, i.e.

~~~text
box(color = vector(1.0, 1.0, 1.0), size = vector(2.0, 1.0, 0.1))
~~~

Try it out! They are in (`length`, `height`, `width`) order. Again, in a `vector` constructor... 


***Task 3: Play around with the three components of the axis...***

Grab the `axis` parameter and place it (after a comma) into the creation of the `box`, i.e.

~~~text
box(color = vector(1.0, 1.0, 1.0), size = vector(2.0, 1.0, 0.1), axis = vector(2.0, 5.0, 1.0))
~~~

Try it out! They are in (`x`, `y`, `z`) order. The size parameter of length is along the axis.
        
Not required: you can specify how width and height are defined via the up parameter.
The documentation for all of this is at the GlowScript reference for `box()` 


Next, you'll try a starting animation with a bit of physics... 

Physics Simulation in `vpython`
--------------------------------

Create a new Python file and paste in the following code (it's lengthy!):

~~~text
from vpython import *
#
# physics_starter.py
#
# Building an interaction with 3D graphics using python
#

# +++ Start of EVENT_HANDLING section -- separate functions for
#                                keypresses and mouse clicks...

def keydown_fun(event):
    """This function is called each time a key is pressed."""
    key = event.key
    print("key pressed:", key)    # Print which key was pressed...

    if key in 'cC':               # Redo the sphere's color...
        ball.color = randcolor()  # Shows how to call your own function...

    elif key in 'rR':             # Redo the sphere's velocity...
        ball.pos = vector(0, 0, 0)         # Reset the ball.pos (position)
        ball.vel = 4.2*vector.random()     # Set a random velocity
        ball.vel.y = 0.0                   # With no y component (no vertical)
        print("velocity is now:", ball.vel)


def click_fun(event):
    """This function is called each time the mouse is clicked."""
    print("event is", event.event, event.which)

# +++ End of EVENT_HANDLING section


# +++ Other functions can go here...

def randcolor():
    """Returns a vector of (r, g, b), randomly selected from 0.0 to 1.0."""
    r = random()   # This is different than Python's random.uniform...
    g = random()   # But is very similar...
    b = random()   # It generates a float between 0.0 and 1.0
    return vector(r, g, b) # A color is a three-element tuple
    # See the next example for implementations of choice and randint

# +++ End of other functions


# +++ Start of SETUP

scene.bind('keydown', keydown_fun)     # Function for key presses
scene.bind('click', click_fun)         # Function for mouse clicks
scene.background = 0.8*vector(1, 1, 1) # Light gray (0.8 out of 1.0)
scene.width = 640                      # Make the 3D canvas larger
scene.height = 480

# +++ End of SETUP


# +++ Start of OBJECT_CREATION section


# The ground is represented by a box (vpython's rectangular solid)
# http://www.glowscript.org/docs/GlowScriptDocs/box.html
# Note that this time we save the thing constructed by "box" in
# a variable named "ground".
ground = box(size = vector(20, 1, 20), pos = vector(0, -1, 0), color = .4*vector(1, 1, 1))

# Show our x and z axes (for labeling and intuition-building)
# http://www.glowscript.org/docs/GlowScriptDocs/label.html
x_axis = arrow(axis = vector(5, 0, 0), color = vector(0, 0, .5))  # dark blue
x_axis_label = label(pos = vec(6, 0, 0), text = 'x', color = vector(0, 0, .5))
# x_axis_text = text(pos = vec(7, 0, 0), text = 'x', color = vector(0, 0, .5))
z_axis = arrow(axis = vector(0, 0, 5), color = vector(0, .5, 0))  # dark green
z_axis_label = label(pos = vec(0, 0, 6), text = 'z', color = vector(0, .5, 0))

# Make a sphere, which is something we will animate.
# http://www.glowscript.org/docs/GlowScriptDocs/sphere.html
# Again, we save the sphere as "ball" so that we can manipulate it later.
ball = sphere(size = 1.0*vector(1, 1, 1), color = vector(0.8, 0.5, 0.0))   # ball is an object of class sphere
ball.vel = vector(4.2, 0, 0)           # This is the initial velocity
print("velocity is now:", ball.vel)    # Printing works as usual


# +++ End of OBJECT_CREATION section


# +++ Start of ANIMATION section

# Other constants
RATE = 30                # The number of times the while loop runs each second
dt = 1.0/RATE            # The time step each time through the while loop
scene.autoscale = False  # Avoids changing the view automatically
scene.forward = vector(0, -3, -2)  # Ask for a bird's-eye view of the scene...
origin = vector(0, 0, 0) # It's nice to have a name for the origin location

# This is the "event loop" or "animation loop"
# Each pass through the loop will animate one step in time, dt
#
while True:

    rate(RATE)   # Maximum number of times per second the while loop runs

    # +++ Start of PHYSICS UPDATES -- update all positions here, every time step


    ball.pos = ball.pos + ball.vel*dt      # distance = rate*time


    # +++ End of PHYSICS UPDATES -- be sure new objects are updated appropriately!


    # +++ Start of COLLISIONS -- check for collisions & do the "right" thing


    # If the ball ventures too far, restart it with a random velocity
    if mag(ball.pos - origin) > 10.0:      # mag == magnitude of a vector
        ball.pos = vector(0, 0, 0)         # Reset the ball.pos (position)
        ball.vel = 4.2*vector.random()     # Set a random velocity
        ball.vel.y = 0.0                   # With no y component (no vertical)
        print("velocity is now:", ball.vel)


    # +++ End of COLLISIONS

~~~

Run it!

Then, match its behavior to the pieces of the code---look over the source, which introduces:

- Some global scene and background variables (based on scene).
- Two objects, ground and ball, of class box and sphere, respectively.
- Some variables to help the animation.
- The `while True` animation loop, or "event loop".
- Some physics (updates and collision checks).
- Two event-handling functions: one for key presses, one for mouse clicks.
  - Hit some keys in the 3D drawing canvas to see what prints... 
- One additional function (that generates a random color). 

Next, in order to feel comfortable and more deeply understand each part of this animation, make these changes to the code and try them out: 

 ***Task 1: [Setup] Change the background color and canvas size***

- Change the value of `scene.background` to change the background color.
  - Neat trick: the expression `0.42*vector(1, 1, 1)` is a fast way to get `vector(0.42, 0.42, 0.42)`, which is dark gray... 
- Change the value of `scene.width` and `scene.height` to adjust your canvas size.
- Try it all out! Errors? Debugging is inevitable...
  - Sometimes, frustratingly, the browser python simply ignores errors---those are trickier to debug!
- Test one change at a time---test often! 


***Task 2: [The objects] Change the moving object from class sphere to something else...***

- Change the class of the moving object from `sphere` to `box`.
  - Don't change the name of the object (that way the "downstream" code will be ok). 
- Try two or more other shapes!
  - The full list is here: http://www.glowscript.org/docs/GlowScriptDocs/primitives.html
  - From that page's left-hand pulldown menu, you can see the details on each shape, i.e., each class ... 
- Feel free to change the initial color, starting position, starting velocity, axis, size, etc.
- Test one change at a time---test often (we might just keep this note around for each task!). 


***Task 3: [Physics updating] Change the universe! (Well, change physics, at least...)***

- Don't change (for now) the set-up variables before the animation loop ("physics loop" or "event loop")
  - `RATE` is the number of frames rendered per second (at least with the browser's best effort).
  - `scene.autoscale = False` means you need to manually zoom (`True` automatically zooms, which is often more annoying than helpful).
  - `scene.forward` is the viewing vector---a good default, for now.
  - `origin` is a point of interest, so we've given it a name (totally optional, but helpful). 
- DO add friction!
  - UNDER the physics-update line, which calculates "distance = rate*time" by writing `ball.pos = ball.pos + ball.vel*dt`
  - Add a second line that multiplies the `ball.vel` vector: `ball.vel = ball.vel * 0.98`
  - Try it! You'll see you've programmed friction into the world! 
- Reverse it! Try `ball.vel = ball.vel * 1.05` for reverse friction.
  - It's nice being able to program your own physics!
  - You may want to remove friction altogether as you continue exploring---it's up to you... 
- Test one change at a time---test often! 


***Task 4: [Collision code] Create collisions and interactions...***

- Next, read over and change the collision-defining part of the code...
- The `mag()` function computes the total magnitude (length) of a vector via the Pythagorean theorem (aka "Euclidean distance")
  - `mag(ball.pos - origin)` thus computes the total distance from `ball.pos` to the `origin`
  - Change the number it's comparing to from `10.0` to `20.0`---try it! 
- Try resetting the ball to a different starting point.
- Try making the reset velocity larger.
- Try commenting out the `ball.vel.y = 0.0` line
  - As always, test one change at a time---test often! 


***Task 5: [Other Functions] Look over the event-handling and other functions at top...***

- Read over the other three functions
- Note that `keydown_fun` uses ball without passing it in!
  - The ball object is a global variable, which means it is automatically accessible to all functions defined after it has been defined. 
- Try changing the printing inside `keydown_fun`---in any way you'd like, to show you have full control here...
  - Try changing that printing line so that you see the newly-defined color's `r`, `g`, `b` components... 
- The other two functions are probably OK as-is, but if you'd like to test different things out, of course, feel free to do so...
  - As always, test one change at a timei---test often! 


All right! You have a constructive sense of how vpython supports physics and physical interactions...

Next, you'll build an interaction (or game...) of your own. But, let's begin from a slightly more sophisticated starting point in the next section... 

Building Your Own Game with `vpython`
--------------------------------------

So, create a new program and paste in the following code (again, it's long):

~~~text
from vpython import *
#
# game_starter.py
#
# Building an interaction with 3D graphics using python
#   Documentation: http://www.glowscript.org/docs/GlowScriptDocs/index.html
#   Examples:      http://www.glowscript.org/#/user/GlowScriptDemos/folder/Examples/
#

# +++ start of EVENT_HANDLING section -- separate functions for
#                                keypresses and mouse clicks...

def keydown_fun(event):
    """This function is called each time a key is pressed."""
    ball.color = randcolor()
    key = event.key
    ri = randint(0, 10)
    print("key:", key, ri)  # Prints the key pressed -- caps only...

    amt = 0.42              # "Strength" of the keypress's velocity changes
    if key == 'up' or key in 'wWiI':
        ball.vel = ball.vel + vector(0, 0, -amt)
    elif key == 'left' or key in 'aAjJ':
        ball.vel = ball.vel + vector(-amt, 0, 0)
    elif key == 'down' or key in 'sSkK':
        ball.vel = ball.vel + vector(0, 0, amt)
    elif key == 'right' or key in "dDlL":
        ball.vel = ball.vel + vector(amt, 0, 0)
    elif key in ' rR':
        ball.vel = vector(0, 0, 0) # Reset! via the spacebar, " "
        ball.pos = vector(0, 0, 0)

def click_fun(event):
    """This function is called each time the mouse is clicked."""
    print("event is", event.event, event.which)

# +++ End of EVENT_HANDLING section

# +++ Other functions can go here...

def choice(L):
    """Implements Python's choice using the random() function."""
    LEN = len(L)              # Get the length
    randomindex = int(LEN*random())  # Get a random index
    return L[randomindex]     # Return that element

def randint(low, hi):
    """Implements Python's randint using the random() function.
       returns an int from low to hi _inclusive_ (so, it's not 100% Pythonic)
    """
    if hi < low:
        low, hi = hi, low               # Swap if out of order!
    LEN = int(hi) - int(low) + 1.       # Get the span and add 1
    randvalue = LEN*random() + int(low) # Get a random value
    return int(randvalue)               # Return the integer part of it

def randcolor():
    """Returns a vector of (r, g, b) random from 0.0 to 1.0."""
    r = random()
    g = random()
    b = random()
    return vector(r, g, b)       # A color is a three-element vector

# +++ End of extra functions

# +++ Start of SETUP

scene.bind('keydown', keydown_fun)     # Function for key presses
scene.bind('click', click_fun)         # Function for mouse clicks
scene.background = 0.8*vector(1, 1, 1) # Light gray (0.8 out of 1.0)
scene.width = 640                      # Make the 3D canvas larger
scene.height = 480

# ++ End of SETUP

# +++ start of OBJECT_CREATION section
# These functions create "container" objects, called "compounds"

def make_alien(starting_position, starting_vel = vector(0, 0, 0)):
    """The lines below make a new "frame", which is a container with a
       local coordinate system.
       The arguments to make_alien allow for any initial starting position
       and initial starting velocity, with a default starting velocity
       of vector(0, 0, 0).

       Compounds can have any number of components.  Here are the
       alien's components:
    """
    alien_body = sphere(size = 1.0*vector(1, 1, 1), pos = vector(0, 0, 0), color = color.green)
    alien_eye1 = sphere(size = 0.3*vector(1, 1, 1), pos = .42*vector(.7, .5, .2), color = color.white)
    alien_eye2 = sphere(size = 0.3*vector(1, 1, 1), pos = .42*vector(.2, .5, .7), color = color.white)
    alien_hat = cylinder(pos = 0.42*vector(0, .9, -.2), axis = vector(.02, .2, -.02), size = vector(0.2, 0.7, 0.7), color = color.magenta)
    alien_objects = [alien_body, alien_eye1, alien_eye2, alien_hat]  # make a list to "fuse" with a compound
    # now, we create a compound -- we'll name it com_alien:
    com_alien = compound(alien_objects, pos = starting_position)
    com_alien.vel = starting_vel   # set the initial velocity
    return com_alien



# The ground is represented by a box (vpython's rectangular solid)
# http://www.glowscript.org/docs/GlowScriptDocs/box.html
ground = box(size = vector(20, 1, 20), pos = vector(0, -1, 0), color = .4*vector(1, 1, 1))

# Create two walls, also boxes
wallA = box(pos = vector(0, 0, -10), axis = vector(1, 0, 0), size = vector(20, 1, .2), color = vector(1.0, 0.7, 0.3)) # amber
wallB = box(pos = vector(-10, 0, 0), axis = vector(0, 0, 1), size = vector(20, 1, .2), color = color.blue)   # blue

# A ball that we will be able to control
ball = sphere(size = 1.0*vector(1, 1, 1), color = vector(0.8, 0.5, 0.0))   # ball is an object of class sphere
ball.vel = vector(0, 0, 0)     # this is its initial velocity

# We make two aliens using two calls to the make_alien function (from above)
alien = make_alien(starting_position = vector(6, 0, -6), starting_vel = vector(0, 0, -1))
alien2 = make_alien(starting_position = vector(-10, 5, -10))  # zero starting velocity


# +++ end of OBJECT_CREATION section


# +++ start of ANIMATION section

# Other constants
RATE = 30                # The number of times the while loop runs each second
dt = 1.0/(1.0*RATE)      # The time step each time through the while loop
scene.autoscale = False  # Avoids changing the view automatically
scene.forward = vector(0, -3, -2)  # Ask for a bird's-eye view of the scene...

# This is the "event loop" or "animation loop"
# Each pass through the loop will animate one step in time, dt
#
while True:

    rate(RATE)   # maximum number of times per second the while loop runs

    # +++ Start of PHYSICS UPDATES -- update all positions here, every time step

    alien.pos = alien.pos + alien.vel*dt   # Update the alien's position
    ball.pos = ball.pos + ball.vel*dt      # Update the ball's position

    # +++ End of PHYSICS UPDATES -- be sure new objects are updated appropriately!


    # +++ Start of COLLISIONS -- check for collisions & do the "right" thing

    # If the ball hits wallA
    if ball.pos.z < wallA.pos.z:  # Hit -- check for z
        ball.pos.z = wallA.pos.z  # Bring back into bounds
        ball.vel.z *= -1.0        # Reverse the z velocity

    # If the ball hits wallB
    if ball.pos.x < wallB.pos.x:  # Hit -- check for x
        ball.pos.x = wallB.pos.x  # Bring back into bounds
        ball.vel.x *= -1.0        # Reverse the x velocity


    # If the ball collides with the alien, give the alien a vertical velocity
    if mag(ball.pos - alien.pos) < 1.0:
        print("To infinity and beyond!")
        alien.color = color.gray(.8)
        alien.vel = vector(0, 1, 0)

    # If the alien ventures too far, restart randomly -- but only if it's
    # not moving vertically.
    if mag(alien.pos) > 10 and alien.vel.y < 1:
        alien.pos.x = choice([-6, 6])
        alien.pos.z = choice([-6, 6])
        alien.vel = 2*vector.random() # Library-supplied random vector
        alien.vel.y = 0.0             # No vertical component of velocity

    # +++ End of COLLISIONS
~~~

Phew! This is a larger chunk of code. Let's look at%G—%@and change---this code piece-by-piece, in order to build an understanding of it. 

***Task 1: [The objects] Read over the object-creation lines and try it out...***

- For now, skip the overall `scene` variables and the `make_alien` function at the top... We'll come back to those.
- Scroll to the object-creation lines:
  - `ground` and `ball`, as before
  - `wallA` and `wallB` are new boxes, with distinct hues (amber and blue)
  - `alien` and `alien2` are new objects that are composites of other objects---cool! We'll handle compositing later... 
- Try the game, using the arrows (or ijkl or wasd) to impart velocity on the ball
  - Note that the arrows correspond to punctuation marks---if your keyboard is different, use the letters instead   (ijkl or wasd) 
- The `alien` is moving under computer control, but the `ball` is under your control
- The goal of the game is to reach the `alien` with the `ball`---if you do, the `alien` ascends and prints a message...
  - That's it! Yes, this game needs work!


So, let's work on it...


***Task 2: [More walls] Creating your own walls and collisions...***

- Your challenge here is to read over the wall-creation code:
  - Figure out how the wall-creation works.
  - Then, create two more walls to finish the "table" or "corral".
  - I'd recommend using distinctive colors for each! 
- Then, read over the wall-collision code:
  - Figure out how the wall-collision code works.
    - Note that the ball's position is corrected so that it's no longer "beyond the wall" each time.
    - This is important---if uncorrected, the ball can get "stuck" inside the wall... 
  - Then, add collisions to your two new walls. 
- Try it! Now, the game will play on its own...
  - The ball will bounce around the corral and eventually encounter the alien... 
- Test often!
  - This becomes more and more important as the game gets larger and larger. 
- Copy your whole program to a file on your desktop (using your text editor, e.g., vscode).
  - The problem with Web-editing like this is that there's no "undo"---aargh!
  - Having a working copy to return to is vital. 


***Task 3: [Your own helper function] Creating your own corral-colliding function...***

- Your challenge here is to take your wall-colliding code and get comfortable making that into its own function.
  - Since there are four walls, making a corral, let's call it corral-colliding...
  - This yields a MAJOR advantage: you'll have ONE corral-colliding function, which EVERY moving object can use! 
- Notice that your corral-colliding lines use the ball variable to check for collisions with the walls
  - We're going to make that an argument to the function instead! 
- To do this, cut your corral-colliding code (probably four if statements with their bodies) and...
  - Paste them into the "other functions" section at the bottom of the file. 
- Add this function-signature line above them:
  - `def corral_collide(ball):` 
- For completeness, add this docstring as well:
~~~text
        """Corral collisions!
           Ball must have a .vel field and a .pos field.
        """
~~~

- THEN, add the line `corral_collide(ball)` back where you had cut the original lines.
  - That line will call the function each time through the animation loop, as needed.
  - You can now add the line `corral_collide(alien)`, too---try it!.
  - To see it working, remove or comment-out the block of code that resets the `alien`.
    - It has a comment: `# if the alien ventures too far, restart randomly`
  - Both the alien and the ball should now bounce around...yay! 

Finally, we can start on...

The Exercise
------------

 You'll be making a 3D do-it-yourself interaction or game!

- You have a palette of 3D "object paints" and a canvas with physics, collisions, and keypresses...
- From here, this lab problem asks you to make changes to this starter code to build your own game or interaction.
- What the game does and how it looks are entirely up to you---but you should include at least TWO of these things (or more---this can become your final project, if you'd like):
  - Add one or more additional non-moving objects in the "playing field" (trees, spaceships, etc. are all fair game to build...).
  - Create at least one new self-moving object   (more aliens---or other things?!).
  - Add one additional interaction between the new objects and the user-controlled object   (collisions or bouncing, as one example).
  - Expand the existing `compound` object or add a new one (see below)   (treating multiple objects as a single whole).
  - Change the user-controlled object (or add another user-controlled object, along with a way to switch between them...) 


And, it is ever so: test often!
As often as you're willing, copy your whole program to a file on your desktop (using your text editor, i.e., vscode).

The problem with Web-editing like this is that there's no "undo" :(


***Compound objects***

- If you'd like to try building or extending your own composite (or `compound`) objects, look over the `make_alien` function near the top of the file...
- It creates several pieces *in their own coordinate system.*
- It makes a list of those pieces and then calls `com_alien = compound(alien_objects, pos = starting_position)`.
  - This creates an object named `com_alien`, which is of class (or type) `compound`.
  - This sticks all of the objects together and gives them a *single existence*---they can no longer be independently manipulated, but the whole thing can be... 

- *To do*: Make your own character!
  - It could be a variation on this one (a third eye, perhaps? or even more detail...).
  - It could be something completely different... 
- Notice that by passing in the `starting_position` vector, the single function can create as many different composite objects as you'd like...
  - This technique is demonstrated by the two aliens in the original... 


***Other helpful functions...***

Below is a `wall_collide(wall, object)` function for walls at any angle in the x-z plane.

It ignores the y components, though you could adapt it to handle those, as well, if you wish. 

~~~text
def wall_collide( w, obj ):
    """ w is a wall
        obj is a moving object
        returns True (and reflects obj.vel) if it collides...
          + ALSO: runs obj.pos = obj.pos - obj.vel*dt to "undo" the collision
        returns False (w/o changing obj) if there's no collision
        all y components are ignored throughout!
    """
    b = obj  # written with the name b, but should be obj!
    wpos_noy = vector(w.pos); wpos_noy.y = 0.0; 
    waxis_noy = vector(w.axis); waxis_noy.y = 0.0; 
    waxis_norm = norm(waxis_noy)
    wperp_norm = rotate(waxis_norm, radians(90), vector(0,1,0))
    bpos_noy = vector(b.pos); bpos_noy.y = 0.0;
    bdiff_noy = bpos_noy - wpos_noy
    bvel_noy = vector(b.vel); bvel_noy.y = 0.0;
    b_axial = dot(waxis_norm,bdiff_noy)
    b_perp = dot(wperp_norm,bdiff_noy)
    b_vel_axial = dot(waxis_norm,bvel_noy)
    b_vel_perp = dot(wperp_norm,bvel_noy)
    
    wLENGTH = abs(w.size.x)/2 # symmetric around the center
    wHEIGHT = abs(w.size.y)/2 # ignored
    wWIDTH = abs(w.size.z)/2  # symmetric around the center
    #print( "L,W:", wLENGTH, wWIDTH, end=" ")
    smallest_dim = max( 0.1, min( wLENGTH, wWIDTH ) )
    
    if mag( wpos_noy - bpos_noy ) < smallest_dim \ 
       or (-wLENGTH < b_axial < wLENGTH and -wWIDTH < b_perp < wWIDTH):
        # hit along the wLENGTH (axis) or...
        #print("ax,perp:", b_axial, b_perp)
        print("In rectangle!")
        b.pos = b.pos - b.vel*dt  # undo last motion
        new_b_vel = b_vel_axial*waxis_norm - b_vel_perp*wperp_norm
        new_b_vel.y = b.vel.y   # recover the y component of the velocity...
        b.vel = new_b_vel
        return True
    else:
        return False
~~~
