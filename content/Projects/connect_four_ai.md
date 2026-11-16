---
title: "Connect Four AI"
date: 2018-07-13T09:46:11-04:00
---

Background
----------
Game AI has a long history---in fact, the field of artificial intelligence (AI) was motivated (in part) by the belief that building programs that could play strategic games well would lead to human-level intelligence.

It turns out that that belief was not true: human-level intelligence is not, fundamentally, about strategic thinking in rule-based contexts like games.

However, the applications of game AI are more than only games. Techniques for finding the best outcome by searching through possible situations (such as game moves) are at the heart of AI and have application in planning problems of many types:

 - Robots planning for what actions or motions to make next.
 - Decision planning that models or simulates complex interactions among artificial agents (and, sometimes, human ones...).
 - Adaptive systems that adjust to user's responses, e.g., for practicing skills in a new field (education and training).

Overview
--------
**The `Board` Class**

Either use your board from [before](/exercises/connect_four) or the starter code below.

{{% expand "Starter Code" %}}
~~~text
class Board(object):
    """
    A datatype representing a Connect Four board with an arbitrary number of rows
    and cols.
    """

    def __init__(self, width=7, height=6):
        """
        Constructor for objects of type Board.
        """
        self.width = width
        self.height = height
        self.data = [[' '] * width for r in range(height)]

    def __repr__(self):
        """
        Returns a string representation for objects of type Board.
        """
        s = '' # accumulator

        # add rows of board
        for row in range(self.height):
            s += '|'
            for col in range(self.width):
                s += self.data[row][col] + '|'
            s += '\n'

        # add divider
        s += '--' * self.width + '-\n'

        # add column labels
        for col in range(self.width):
            s += ' ' + str(col%10)
        s += '\n'

        return s

    def set_board(self, moves, show=True):
        """
        Sets the board state according to a string of turns (moves), starting
        with 'X'. Print the board after each move if show is True. Does NOT
        check for wins between move.
        """
        next = 'X'
        for move in moves:
            # coax int from move string
            col = int(move)

            # check move validity
            if self.allows_move(col):
                self.add_move(col, next)

            # other player's turn
            if next == 'X':
                next = 'O'
            else:
                next = 'X'

            if show:
                print(self)

    def clear(self):
        """
        Clear the board.
        """
        # iterate over every spot in board using indices
        for row in range(self.height):
            for col in range(self.width):
                # clear every spot
                self.data[row][col] = ' '

    def is_ox(self, row, col, ox):
        """
        Returns True if the spot at row and col is legal and ox. Returns False,
        otherwise.
        """
        # check if spot at row and col is in bounds
        if 0 <= row < self.height and 0 <= col < self.width:
            # if in bounds, checker whether contains ox checker
            return self.data[row][col] == ox

        return False

    def allows_move(self, col):
        """
        Returns True if a move to col is allowed in the Board represented by
        self. Returns False, otherwise
        """
        # check if col out of bounds
        if col < 0 or col >= self.width:
            return False

        # if col in bounds, return whether it's not full
        return self.data[0][col] == ' '

    def add_move(self, col, ox):
        """
        Adds checker ox into column col. Does not check for move validity.
        """
        row = self.height - 1

        # iterate over row indices from the bottom up
        while row >= 0:
            # add checker at first empty spot
            if self.data[row][col] == ' ':
                self.data[row][col] = ox
                return
            row -= 1

    def del_move(self, col):
        """
        Removes the top checker from column col, if non-empty.
        """
        # iterate over row indices from the top down
        for row in range(self.height):
            # clear the first non-empty spot
            if self.data[row][col] != ' ':
                self.data[row][col] = ' '
                return

    def wins_for(self, ox):
        """
        Returns whether the board is in a winning state for player using the
        ox checker.
        """
        # iterate over every spot in board using indices
        for row in range(self.height):
            for col in range(self.width):
                # check for winning streaks at every position
                if (
                    self.check_down_left(row, col, ox)  or
                    self.check_down_right(row, col, ox) or
                    self.check_down(row, col, ox)      or
                    self.check_right(row, col, ox)
                ):
                    return True
        return False

    def check_down_left(self, y, x, ox):
        if x >= 3 and y < self.height - 3:
            return [self.data[y+i][x-i] for i in range(4)] == [ox] * 4
        return False

    def check_down_right(self, y, x, ox):
        if x < self.width - 3 and y < self.height - 3:
            return [self.data[y+i][x+i] for i in range(4)] == [ox] * 4
        return False

    def check_down(self, y, x, ox):
        if y < self.height - 3:
            return [self.data[y+i][x] for i in range(4)] == [ox] * 4
        return False

    def check_right(self, y, x, ox):
        if x < self.width - 3:
            return self.data[y][x:x+4] == [ox] * 4
        return False

    def is_full(self):
        """
        Returns True if the board is completely full. Returns False, otherwise.
        """
        # iterate over columns
        for col in range(self.width):
            # board is not full if a move can be made in any column
            if self.allows_move(col):
                return False

        # if no valid moves found, board is full
        return True

    def game_over(self):
        """
        Returns True if the game is over. Returns False, otherwise.
        """
        # if either case is True, game is over
        return self.is_full() or self.wins_for('X') or self.wins_for('O')

    def host_game(self):
        """
        Hosts a game of Connect Four between two human players.
        """
        next = 'X'
        while True:
            # print the board
            print(self)

            # get the next move from the player
            col = -1
            while not self.allows_move(col):
                try:
                    col = int(input('Next col for ' + next + ': '))
                except ValueError: # if non-number input, just keep asking
                    continue

            # once valid move specified, make move
            self.add_move(col, next)

            # check if move wins game
            if self.wins_for(next):
                print(self)
                print('\n' + next + ' wins! Congratulations!\n\n')
                break

            # check if move filled board
            if self.is_full():
                print(self)
                print('\nThe game is a draw.\n\n')
                break

            # make other player's turn
            if next == 'X':
                next = 'O'
            else:
                next = 'X'

        print('Thanks for playing!')

    def play_game(self, player_X, player_O, ss=False):
        """
        Plays a game of Connect Four.  player_X and player_O are objects of type
        Player OR the string 'human'.  If ss is True, it will "show scores" each
        time.
        """

        next_checker = 'X'
        next_player = player_X

        while True:
            # print the board
            print(self)

            if next_player == 'human': # human player
                col = -1
                while not self.allows_move(col):
                    try:
                        col = int(input('Next col for ' + next_checker + ': '))
                    except ValueError:
                        continue
            else: # non-human player
                if ss:
                    scores = next_player.scores_for(self)
                    print(next_checker + "'s", 'Scores:', end=' ')
                    print([int(sc) for sc in scores])
                    col = next_player.tiebreak_move(scores)
                else:
                    col = next_player.next_move(self)

            # add the checker to the board
            self.add_move(col, next_checker)

            # check if move wins game
            if self.wins_for(next_checker):
                print(self)
                print('\n' + next_checker + ' wins! Congratulations!\n\n')
                break

            # check if move filled board
            if self.is_full():
                print(self)
                print('\nThe game is a draw.\n\n')
                break

            # other player's turn
            if next_checker == 'X':
                next_checker = 'O'
                next_player = player_O
            else:
                next_checker = 'X'
                next_player = player_X

        print('Thanks for playing!')
~~~
{{% /expand %}}

**The `Player` Class**

The main focus of this project is to implement another class related to Connect Four. You should add the `Player` class in the same file as the `Board` class.

The job of the `Player` class is to evaluate Connect Four board states and decide what move to make. The basic approach is as follows:

 1. Look at each column on the board. Give each column a numeric score.
    - `-1.0` for a column that is full.
    - `0.0` for a column that, if chosen, results in a loss.
    - `50.0` for a column that, if chosen, doesn't immediately lead to a win or
      loss.
    - `100.0` for a column that, if chosen, results in a win.
 2. Make a move using the column with the greatest score. If the maximum score is held by more than one column, one of the following strategies is used:
    - `'LEFT'` picks the leftmost high score.
    - `'RIGHT'` picks the rightmost high score.
    - `'RANDOM'` picks one of the high scores randomly.

Implementing the `Player` Class
-------------------------------

Your `Player` class should have at least these three data attributes:

 - A one-character string representing the checker, either 'X' or 'O', being
   used by the Connect Four `Player`.
{{% notice warning %}}
Remember to be careful to use `'O'` the capital letter, not zero!
{{% /notice %}}
 - A string, either `'LEFT'`, `'RIGHT'`, or `'RANDOM'`, representing the tiebreaking type of the `Player`. This is the name for one of the three strategies described above.
 - A nonnegative integer representing how many moves into the future the player will look in order to evaluate possible moves. We'll refer to this quantity as `ply`.

Your `Player` class should have the following methods:

### `def __init__(self, ox, tbt, ply):`

This is a constructor for `Player` objects that takes three arguments. First, it takes in a one-character string `ox`. This will be either `'X'` or `'O'`. Second, it takes in `tbt`, a string representing the tiebreaking type of the `Player`. It will be one of `'LEFT'`, `'RIGHT'`, or `'RANDOM'`. Third, `ply`, is a nonnegative integer representing the number of moves that the player should look into the future when evaluating where to go next.

Inside the constructor, you should set the values of the object's data attributes. There's not much else for this method.

### `def __repr__(self):`

This method returns a string representing the `Player` object that calls it. This should simply print the three important characteristics of the object: its checker string, its tiebreaking type, and its ply.

### `def opp_ch(self):`

This method should return the other kind of checker or playing piece, i.e., the piece being played by `self`'s opponent. In particular, if `self` is playing `'X'`, this method returns `'O'` and vice-versa.

### `def score_board(self, b):`

This method should return a single float value representing the score of the input `b`, which you may assume will be an object of type `Board`. This should return `100.0` if the `Board` `b` is a win for `self`. It should return `50.0` if it is neither a win nor a loss for `self`, and it should return `0.0` if it is a loss for `self` (i.e., the opponent has won).

### `def tiebreak_move(self, scores):`

This method takes in `scores`, which will be a nonempty list of floating-point numbers. If there is only one highest score in that `scores` list, this method should return its column number, not the actual score! Note that the column number is the same as the index into the list `scores`. If there is more than one highest score because of a tie, this method should return the column number of the highest score appropriate to the `Player`'s tiebreaking type.

Thus, if the tiebreaking type is `'LEFT'`, then `tiebreak_move` should return the column of the leftmost highest score (not the score itself). If the tiebreaking type is `'RIGHT'`, then `tiebreak_move` should return the column of the rightmost highest score (not the score itself). And if the tiebreaking type is `'RANDOM'`, then `tiebreak_move` should return the column of the a randomly-chosen highest score (yet again, not the score itself).

One possible way to write this method is to first create a list of indices at which scores contains its max element. For example, if `scores` consisted of `[50, 50, 50, 50, 50, 50, 50]`, then `max_indices` would be `[0, 1, 2, 3, 4, 5, 6]`. On the other hand, if `scores` was the list `[50, 100, 100, 50, 50, 100, 50]`, then `max_indices` would be `[1, 2, 5]`.

### `def scores_for(self, b):`

This method is the heart of the `Player` class! Its job is to return a list of scores, with the cth score representing the "goodness" of the input board after the player moves to column c. And, "goodness" is measured by what happens in the game after `self.ply` moves are made.

Admittedly, that is a lot to handle! So, here is a breakdown:

1. Create a list (maybe called `scores`) with length equal to the number of columns in the `Board` `b`, with every element set to `50`. Remember that you can use list multiplication: `[50] * b.width`.

2. Iterate over all possible columns:

> **Base Case**<br>
> If a particular column is full, it assigns a `-1.0` score for that column.
>
> **Base Case**<br>
> If the game has already been won for `self`, then there's no point in making any additional moves (indeed, it's not allowed!) simply use the appropriate score ( `100.0` ) for the current column under consideration.
>
> **Base Case**<br>
> If the game has already been won for `self.opp_ch()`, then there's also no point in making any additional moves. Simply use the approproate score ( `0` ) for the current column under consideration. It's important that the check for `self`'s win occurs before the check for the opponent's win, because there are boards where both are true—but `self` gets to move first!
>
> **Base Case**<br>
> If the object's `ply` is `0`, no move is made. What's more, if you've handled the "column full" and "game over" cases above, there's only one score left to give the column with a `ply` of `0`.
>
> **Recursive Case**<br>
> If the object's `ply` is greater than `0` and the game isn't over, the code should make a move into the column that is under consideration. This will use some of the methods in `Board`. In addition, it's a good idea to check if the new, resulting board has ended the game. If so, give the column the appropriate score.

Once that move is made, if the game is not over, the crucial task is to determine what scores an opponent would give the resulting board.

This means creating an opponent (which will be of `Player` class!). How to create an opponent? You can simply establish a new object of type `Player`! For example, `op = Player(self.opp_ch(), ..., ...)`. It's safe to assign this to-be-constructed opponent `Player` the same tiebreaking-style as you use---that is, the same as `self.tbt`. What is the correct value of `ply` to give it? Once you've created an opposing `Player`, you should use recursion to obtain the seven scores that the opponent would give to its next move.

However, the scores reported by the opponent are NOT the scores that `self` should use! After all, the opponent has a different goal than `self`! Rather, you will want to figure out which score out of the seven the opponent, `op`, would choose. Then, compute the score you (`self`) would obtain: this will be `100` minus the opponent's best score. Finally, assign the resulting score to the value of the current column's move.

Be sure to delete the checker that had been placed throughout the evaluation of this particular column!

Once all of the possible moves have been evaluated, the `scores_for` method should return the complete list of scores, one per column. So, in a seven-column board, there will be seven numbers in the list returned.

### `def next_move(self, b):`

This method accepts `b`, an object of type `Board`, and returns an integer---namely, the column number that the calling object (of class `Player`) chooses to move to. This is the primary interface to `Player`, but it is really just a "wrapper" for the heavy lifting done by the other methods, particularly `scores_for`. Thus, `next_move` should use `scores_for` and `tiebreak_move` to return its move.

### `def play_game(self, px, po):`

This method calls the `next_move` method for two objects of type `Player` in order to play a game. Those objects are named `px` and `po`.

{{% notice note %}}
Feel free to write `play_game` on your own, if you'd like the challenge! Or, feel equally free to use the one that's in the starter code provided above.
{{% /notice %}}

Either way, there's one additional twist to `play_game`: you should test your Connect Four-playing code by playing games both against itself and against a person. That is, if `px` or `po` is the string `'human'` instead of an object of type `Player`, then `play_game` pauses and asks the user to input the next column to move for that player, with error checking just as in `host_game`.

Testing the `Player` Class
--------------------------

### `__init__` and `__repr__`
~~~text
>>> p = Player('X', 'LEFT', 2)
>>> p
Player for X
  with tiebreak type: LEFT
  and ply == 2

>>> p = Player('O', 'RANDOM', 0)
>>> p
Player for O
  with tiebreak type: RANDOM
  and ply == 0
~~~

### `opp_ch`
~~~text
>>> p = Player('X', 'LEFT', 3)
>>> p.opp_ch()
'O'

>>> Player('O', 'LEFT', 0).opp_ch()
'X'
~~~

### `score_board`
~~~text
>>> b = Board(7, 6)
>>> b.set_board('01020305')
>>> b

| | | | | | | |
| | | | | | | |
|X| | | | | | |
|X| | | | | | |
|X| | | | | | |
|X|O|O|O| |O| |
---------------
 0 1 2 3 4 5 6

>>> p = Player('X', 'LEFT', 0)
>>> p.score_board(b)
100.0

>>> Player('O', 'LEFT', 0).score_board(b)
0.0

>>> Player('O', 'LEFT', 0).score_board(Board(7, 6))
50.0
~~~

### `tiebreak_move`
~~~text
>>> scores = [0, 0, 50, 0, 50, 50, 0]

>>> p = Player('X', 'LEFT', 1)
>>> p2 = Player('X', 'RIGHT', 1)

>>> p.tiebreak_move(scores)
2

>>> p2.tiebreak_move(scores)
5
~~~

### `scores_for`
~~~text
>>> b = Board(7, 6)
>>> b.set_board('1211244445')
>>> b

| | | | | | | |
| | | | | | | |
| | | | |X| | |
| |O| | |O| | |
| |X|X| |X| | |
| |X|O| |O|O| |
---------------
 0 1 2 3 4 5 6
~~~

0-ply lookahead doesn't see threats...

~~~text
>>> Player('X', 'LEFT', 0).scores_for(b)
[50.0, 50.0, 50.0, 50.0, 50.0, 50.0, 50.0]
~~~

1-ply lookahead sees immediate wins (if only it were 'O's turn!)

~~~text
>>> Player('O', 'LEFT', 1).scores_for(b)
[50.0, 50.0, 50.0, 100.0, 50.0, 50.0, 50.0]
~~~

2-ply lookahead sees possible losses ('X' better go to column 3...)

~~~text
>>> Player('X', 'LEFT', 2).scoresFor(b)
[0.0, 0.0, 0.0, 50.0, 0.0, 0.0, 0.0]
~~~

3-ply lookahead sees set-up wins ('X' sees that col 3 is a win!)

~~~text
>>> Player('X', 'LEFT', 3).scores_for(b)
[0.0, 0.0, 0.0, 100.0, 0.0, 0.0, 0.0]
~~~

At 3-ply, 'O' does not see any danger if it moves to columns on either side...

~~~text
>>> Player('O', 'LEFT', 3).scores_for(b)
[50.0, 50.0, 50.0, 100.0, 50.0, 50.0, 50.0]
~~~

But at 4-ply, 'O' does see the danger! Again, too bad it's not 'O's turn...

~~~text
>>> Player('O', 'LEFT', 4).scores_for(b)
[0.0, 0.0, 0.0, 100.0, 0.0, 0.0, 0.0]
~~~

### `next_move`
~~~text
>>> b = Board(7, 6);
>>> b.set_board('1211244445')
>>> b

| | | | | | | |
| | | | | | | |
| | | | |X| | |
| |O| | |O| | |
| |X|X| |X| | |
| |X|O| |O|O| |
---------------
 0 1 2 3 4 5 6

>>> Player('X', 'LEFT', 1).next_move(b)
0

>>> Player('X', 'RIGHT', 1).next_move(b)
6

>>> Player('X', 'LEFT', 2).next_move(b)
3

>>> Player('X', 'RIGHT', 2).next_move(b)
3

>>> Player('X', 'RANDOM', 2).next_move(b)
3
~~~

### `play_game`

Some deterministic examples:

~~~text
>>> px = Player('X', 'LEFT', 0)
>>> po = Player('O', 'LEFT', 0)
>>> b = Board(7, 6)
>>> b.play_game(px, po)

 ...

|O|O|O| | | | |
|X|X|X| | | | |
|O|O|O| | | | |
|X|X|X| | | | |
|O|O|O| | | | |
|X|X|X|X| | | |
---------------
 0 1 2 3 4 5 6

X wins!
~~~

~~~text
>>> px = Player('X', 'LEFT', 1)
>>> po = Player('O', 'LEFT', 1)
>>> b = Board(7, 6)
>>> b.play_game(px, po)

 ...

|O|O| | | | | |
|X|X| | | | | |
|O|O| | | | | |
|X|X| | | | | |
|O|O|O| | | | |
|X|X|X|X| | | |
---------------
 0 1 2 3 4 5 6

X wins!
~~~

~~~text
>>> px = Player('X', 'LEFT', 3)
>>> po = Player('O', 'LEFT', 2)
>>> b = Board(7, 6)
>>> b.play_game(px, po)

 ...

|O|O|X|X|O|O| |
|X|X|O|O|X|X| |
|O|O|X|X|O|O| |
|X|X|O|O|X|X| |
|O|O|X|O|O|O|O|
|X|X|X|O|X|X|X|
---------------
 0 1 2 3 4 5 6

O wins!
~~~


Extensions
----------
You can choose one of the three extensions to add to your Connect Four.

### Graphics
For this extension, use `pygame` to create a playable version of Connect Four—along with your AI.

The design of this is up to you, but your result should:
- Allow the user to play either 'X' or 'O' (however they're represented).
- Allow the user to choose a difficulty level (the `ply` level at which the AI plays).
- Allow the user to tell the computer to play against itself (at two different levels, if desired).
- And, it should play against the user and recognize when the game ends in a win, loss, or tie.

Details are wide open here---we welcome your creatively-themed Connect-Four implementations.

Be sure to include a description of how to play your Connect Four!

### Static Board Evaluation for AI
Since n-ply lookahead is the same for every player, AIs vary not based on their search, but on their evaluation of the board at the end of the search—i.e., when the game is neither a win nor a loss.

Our overview, above, suggests weighting those boards at 50 (on a 0-100 scale), but much more sophistication is possible. A function that is more careful about scoring these non-win/non-loss board states is sometimes called the "static board evaluator," because it looks only at the board's current status. It's these static evaluators that distinguish the abilities of two different game AIs. Static board evaluation tries to capture humans' "intuition" about a game, and it is used by all computer game-players in all types of games, from Hydra, a very good computer chess player to Go-playing programs. Things like computer poker players do the same thing, but they model more than just the game state. The probabilities of future states, along with the tendencies of other players, are modeled as well.

So, for this option, you should allow the user to play in two different modes: plain evaluation (how the AI works now) or savvy evaluation.

With the savvy evaluation, you will implement a static-board-evaluation function that is more sophisticated than the 0-50-100 version.

Here, create a new `score_board_tourney` function (but save the old one, in case anything goes wrong!)

This new `score_board_tourney` should return a more accurate evaluation of how good or bad board `b` is for `self.ox`—more accurate than the simple 0-50-100 scoring of the default Player used.

The new `score_board_tourney(self, b)` may NOT look further ahead into possible future moves—rather, it should take into account factors like:

- How central are my pieces compared to my opponents' pieces?
- Do I have any (unblocked) 2-in-a-row runs? Or does my opponent?
- Similarly for (unblocked) 3-in-a-row runs.
- And any other factor about the current board you might want to compute...

The only constraint on `score_board_tourney(self, b)` function is that it should return a number (a float) for each board provided, with higher numbers indicating a better board (for `self.ox`). Since this is evaluating a board and not a column, it's ok to use negative numbers to represent really bad boards... That said, some people find it easier to reason about board-scores on a 0-100 range (0 = loss, 100 = win). Also, you should assume the board will be 7 columns and 6 rows, as in the standard version of the game.

You're welcome to use randomness in `score_board_tourney(self, b)` function, if you'd like.

How to test your `score_board_tourney` function?

> Copy-and-paste your `scores_for` method and name the copy `scores_for_tourney`. Change the old code:
>
> ~~~text
> elif self.ply == 0:
>     scores[col] = 50.0
> ~~~
>
> To the new version:
>
> ~~~text
> elif self.ply == 0:
>     scores[col] = self.score_board_tourney(b)
> ~~~
>
> and then play against it yourself or play it against other players you construct from the `Player` class.

Be sure to print out the scores you're computing, to see if they match your intuition!

### Your Own Game
For this option, revise the rules of Connect Four. Or, even more ambitiously, you're welcome to create another two-player game—presumably one that uses a 1d or 2d board!

Then, adapt the Board and Player classes to implement your alternative game! Be sure to do this in a different Player and/or Board class: choose a new name that fits!

If you'd like to take this path, we would recommend changing the rules of Connect Four—at least at first. For example, you could add any one of these variations:

- Add a chance (perhaps 10%) that the game randomly ignores the move you choose and chooses a different allowable move...
- Randomly swap an X with an O every once in a while!
- Allow the user to "flip" the board—as if it rotated 180 degrees (and the checkers don't fall out!)
- Have a row of checkers disappear when it's entirely full (Tetris-style—leads to interesting strategies!)
- Have gravity go "diagonally" !
- Many other variants are welcome (and, importantly, feasible...)


Be sure to include a note explaining your game and how to play.

If you choose this extension, free to simply add more classes to you Python file—or include a second `.py` file...
