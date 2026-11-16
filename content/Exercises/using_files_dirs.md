---
title: "Working with Files and Directories"
date: 2018-06-12T10:04:08-04:00
weight: 300
---

Objectives
----------
- Create a directory hierarchy that matches a given diagram.

- Create files in that hierarchy using an editor or by copying and renaming
  existing files.

- Delete specified files and/or directories.

Background
----------
We now know how to explore files and directories, but how do we create them in
the first place?  Let's go back to our `data-shell` directory on the Desktop and
use `ls` to see what it contains:

~~~text
$ ls

creatures  data  molecules  north-pacific-gyre  notes.txt  pizza.cfg  solar.pdf  writing
~~~

Let's create a new directory called `thesis` using the command `mkdir thesis`
(which has no output):

~~~text
$ mkdir thesis
~~~

As you might guess from its name, `mkdir` means "make directory".  Since
`thesis` is a relative path (i.e., doesn't have a leading slash), the new
directory is created in the current working directory:

~~~text
$ ls

creatures  data  molecules  north-pacific-gyre  notes.txt  pizza.cfg  solar.pdf  thesis  writing
~~~

{{% notice note %}}
**Two Ways Of Doing The Same Thing**
<br>
Using the shell to create a directory is no different than using a file
explorer.  If you open the current directory using your operating system's
graphical file explorer, the `thesis` directory will appear there too.  While
they are two different ways of interacting with the files, the files and
directories themselves are the same.
{{% /notice %}}

Naming Files and Directories
----------------------------
Complicated names of files and directories can make your life painful when
working on the command line. Here we provide a few useful tips for the names of
your files.

{{% notice tip %}}
**Don't Use Whitespaces**
<br>
Whitespaces can make a name more meaningful but since whitespace is used to
break arguments on the command line it is better to avoid them in names of files
and directories.  You can use `-` or `_` instead of whitespace.
{{% /notice%}}

{{% notice warning %}}
**Don't Begin Names With Dashes ( `-` )**
<br>
Commands treat names starting with `-` as flags.
{{% /notice %}}

{{% notice tip %}}
**Safe Characters For Naming**
Stick With letters, numbers, periods ( `.` ), dashes ( `-` ) and underscores (
`_` ). Many other characters have special meanings on the command line.  We will
learn about some of these during this lesson.  There are special characters that
can cause your command to not work as expected and can even result in data loss.
<br><br>
If you need to refer to names of files or directories that have whitespace or
another non-alphanumeric character, you should surround the name in double
quotes (`"`).
{{% /notice %}}

Since we've just created the `thesis` directory, there's nothing in it yet:

~~~text
$ ls thesis
~~~

Let's change our working directory to `thesis` using `cd`, then run a text
editor called **Visual Studio Code**, with the command `code`, to create a file
called `draft.txt`:

~~~text
$ cd thesis
$ code draft.txt
~~~

This will open up Visual Studio Code with `draft.txt` open!

Which Editor?
-------------
When we talk about a text editor, we really do mean "text": it can only work
with plain character data, not tables, images, or any other human-friendly
media.

We will be learning how to use [Visual Studio
Code](https://code.visualstudio.com/) and its various tools in [exercise
6](../using_vscode)!

There are many other GUI editors out there, and even a few command line editors
like [Vim](https://www.vim.org/) and
[Emacs](https://www.gnu.org/software/emacs/).

No matter what editor you use, you will need to know where it searches for and
saves files. If you start it from the shell, it will (probably) use your current
working directory as its default location. If you use your computer's start
menu, it may want to save files in `~/Desktop` or `~/Documents` instead.  You
can change this by navigating to another directory the first time you "Save
As..."

Let's type in a few lines of text.  Once we're happy with our text, we can press
<kbd>Ctrl</kbd>-<kbd>S</kbd> (press the <kbd>Ctrl</kbd> key and, while holding
it down, press the <kbd>S</kbd> key) to write our data to disk (i.e. save).

{{% notice note %}}
**Control, Ctrl, or ^ Key**
<br>
The Control key is also called the "Ctrl" key. There are various ways in which
using the Control key may be described. For example, you may see an instruction
to press the Control key and, while holding it down, press the X key, described
as any of:
<br><br>
`Control-X`
<br>
`Control+X`
<br>
`Ctrl-X`
<br>
`Ctrl+X`
<br>
`^X`
<br>
`C-x`
{{% /notice %}}

Visual Studio Code doesn't leave any output on the screen after it exits, but
`ls` now shows that we have created a file called `draft.txt`:

~~~text
$ ls

draft.txt
~~~

> *Challenge*: Creating Files a Different Way
> -------------------------------------------
> We have seen how to create text files by opening a text editor.  Now, try the
> following command in your home directory:
>
~~~text
$ cd
$ touch my_file.txt
~~~
>
> 1. What did the `touch` command do?  When you look at your home directory
>    using the GUI file explorer, does the file show up?
>
> 2. Use `ls -l` to inspect the files.  How large is `my_file.txt`?
>
> 3. When might you want to create a file this way?
>
{{% expand "Solution" %}}
1. The `touch` command generates a new file called `my_file.txt` in your home
   directory.  If you are in your home directory, you can observe this newly
   generated file by typing `ls` at the command line prompt.  `my_file.txt` can
   also be viewed in your GUI file explorer.

2. When you inspect the file with `ls -l`, note that the size of `my_file.txt`
   is 0kb.  In other words, it contains no data.  If you open `my_file.txt`
   using your text editor it is blank.

3. Some programs do not generate output files themselves, but instead require
   that empty files have already been generated.  When the program is run, it
   searches for an existing file to populate with its output.  The `touch`
   command allows you to efficiently generate a blank text file to be used by
   such programs.
{{% /expand %}}
>

Returning to the `data-shell` directory, let's tidy up the `thesis` directory by
removing the draft we created:

~~~text
$ cd thesis
$ rm draft.txt
~~~

This command removes files (`rm` is short for "remove").  If we run `ls` again,
its output is empty once more, which tells us that our file is gone:

~~~text
$ ls
~~~

Deleting Is Forever
-------------------
The Unix shell doesn't have a trash bin that we can recover deleted files from
(though most graphical interfaces to Unix do).  Instead, when we delete files,
they are unhooked from the file system so that their storage space on disk can
be recycled. Tools for finding and recovering deleted files do exist, but
there's no guarantee they'll work in any particular situation, since the
computer may recycle the file's disk space right away.

Let's re-create that file and then move up one directory to `data-shell` using
`cd ..`:

~~~text
$ pwd

/home/nelle/Desktop/data-shell/thesis
~~~

~~~text
$ code draft.txt
$ ls

draft.txt
~~~

~~~text
$ cd ..
~~~

If we try to remove the entire `thesis` directory using `rm thesis`, we get an
error message:

~~~text
$ rm thesis

rm: cannot remove `thesis': Is a directory
~~~

This happens because `rm` by default only works on files, not directories.

To really get rid of `thesis` we must also delete the file `draft.txt`.  We can
do this with the [recursive](https://en.wikipedia.org/wiki/Recursion) option for
`rm`:

~~~text
$ rm -r thesis
~~~

Using `rm` Safely
-----------------
What happens when we type `rm -i thesis/quotations.txt`?

Why would we want this protection when using `rm`?

~~~text
$ rm: remove regular file 'thesis/quotations.txt'?
~~~

The `-i` option will prompt before every removal.  The Unix shell doesn't have a
trash bin, so all the files removed will disappear forever.  By using the `-i`
flag, we have the chance to check that we are deleting only the files that we
want to remove.

With Great Power Comes Great Responsibility
-------------------------------------------
Removing the files in a directory recursively can be a very dangerous operation.
If we're concerned about what we might be deleting we can add the "interactive"
flag `-i` to `rm` which will ask us for confirmation before each step.

~~~text
$ rm -ri thesis
rm: descend into directory "thesis"? y
rm: remove regular file "thesis/draft.txt"? y
rm: remove directory "thesis"? y
~~~

This removes everything in the directory, then the directory itself, asking at
each step for you to confirm the deletion by typing "y" and hitting
<kbd>Enter</kbd>.

Let's create that directory and file one more time.  (Note that this time we're
running `code` with the path `thesis/draft.txt`, rather than going into the
`thesis` directory and running `code` on `draft.txt` there.)

~~~text
$ pwd

/home/nelle/Desktop/data-shell
~~~

~~~text
$ mkdir thesis
$ code thesis/draft.txt
$ ls thesis

draft.txt
~~~

`draft.txt` isn't a particularly informative name, so let's change the file's
name using `mv`, which is short for "move":

~~~text
$ mv thesis/draft.txt thesis/quotes.txt
~~~

The first argument tells `mv` what we're "moving", while the second is where
it's to go.  In this case, we're moving `thesis/draft.txt` to
`thesis/quotes.txt`, which has the same effect as renaming the file.  Sure
enough, `ls` shows us that `thesis` now contains one file called `quotes.txt`:

~~~text
$ ls thesis

quotes.txt
~~~

One has to be careful when specifying the target file name, since `mv` will
silently overwrite any existing file with the same name, which could lead to
data loss. An additional flag, `mv -i` (or `mv --interactive`), can be used to
make `mv` ask you for confirmation before overwriting.

Just for the sake of consistency, `mv` also works on directories

Let's move `quotes.txt` into the current working directory.  We use `mv` once
again, but this time we'll just use the name of a directory as the second
argument to tell `mv` that we want to keep the filename, but put the file
somewhere new.  (This is why the command is called "move".) In this case, the
directory name we use is the special directory name `.` that we mentioned
earlier.

~~~text
$ mv thesis/quotes.txt .
~~~

The effect is to move the file from the directory it was in to the current
working directory.  `ls` now shows us that `thesis` is empty:

~~~text
$ ls thesis
~~~

Further, `ls` with a filename or directory name as an argument only lists that
file or directory.  We can use this to see that `quotes.txt` is still in our
current directory:

~~~text
$ ls quotes.txt

quotes.txt
~~~

> *Challenge*: Moving to the Current Folder
> -----------------------------------------
> After running the following commands, Jamie realizes that she put the files
> `sucrose.dat` and `maltose.dat` into the wrong folder:
>
~~~text
$ ls -F

analyzed/ raw/

$ ls -F analyzed

fructose.dat glucose.dat maltose.dat sucrose.dat

$ cd raw/
~~~
>
> Fill in the blanks to move these files to the current folder (i.e., the one
> she is currently in):
>
~~~text
$ mv ___/sucrose.dat  ___/maltose.dat ___
~~~
>
{{% expand "Solution" %}}
~~~text
$ mv ../analyzed/sucrose.dat ../analyzed/maltose.dat .
~~~
{{% /expand %}}
>
> Recall that `..` refers to the parent directory (i.e. one above the current
> directory) and that `.` refers to the current directory.

Copying
-------
The `cp` command works very much like `mv`, except it copies a file instead of
moving it.  We can check that it did the right thing using `ls` with two paths
as arguments --- like most Unix commands, `ls` can be given multiple paths at
once:

~~~text
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt

quotes.txt   thesis/quotations.txt
~~~

To prove that we made a copy, let's delete the `quotes.txt` file in the current
directory and then run that same `ls` again.

~~~text
$ rm quotes.txt
$ ls quotes.txt thesis/quotations.txt

ls: cannot access quotes.txt: No such file or directory

thesis/quotations.txt
~~~

This time it tells us that it can't find `quotes.txt` in the current directory,
but it does find the copy in `thesis` that we didn't delete.

What's In A Name?
-----------------
You may have noticed that all of Nelle's files' names are "something dot
something", and in this part of the lesson, we always used the extension `.txt`.
This is just a convention: we can call a file `mythesis` or almost anything else
we want. However, most people use two-part names most of the time to help them
(and their programs) tell different kinds of files apart. The second part of
such a name is called the **filename extension**, and indicates what type of
data the file holds: `.txt` signals a plain text file, `.pdf` indicates a PDF
document, `.cfg` is a configuration file full of parameters for some program or
other, `.png` is a PNG image, and so on.

This is just a convention, albeit an important one. Files contain bytes: it's up
to us and our programs to interpret those bytes according to the rules for plain
text files, PDF documents, configuration files, images, and so on.

Naming a PNG image of a whale as `whale.mp3` doesn't somehow magically turn it
into a recording of whalesong, though it *might* cause the operating system to
try to open it with a music player when someone double-clicks it.

> *Challenge*: Renaming Files
> ---------------------------
> Suppose that you created a `.txt` file in your current directory to contain a
> list of the statistical tests you will need to do to analyze your data, and
> named it: `statstics.txt`
>
> After creating and saving this file you realize you misspelled the filename!
> You want to correct the mistake, which of the following commands could you use
> to do so?
>
> 1. `cp statstics.txt statistics.txt`
> 2. `mv statstics.txt statistics.txt`
> 3. `mv statstics.txt .`
> 4. `cp statstics.txt .`
>
{{% expand  "Solution" %}}
1. No.  While this would create a file with the correct name, the incorrectly
   named file still exists in the directory and would need to be deleted.
2. Yes, this would work to rename the file.
3. No, the period ( `.` ) indicates where to move the file, but does not provide
   a new file name; identical file names cannot be created.
4. No, the period ( `.` ) indicates where to copy the file, but does not provide
   a new file name; identical file names cannot be created.
{{% /expand %}}
>

<br>

> *Challenge*: Moving and Copying
> -------------------------------
> What is the output of the closing `ls` command in the sequence shown below?
>
~~~text
$ pwd

/home/jamie/data
~~~
>
~~~text
$ ls

proteins.dat
~~~
>
~~~text
$ mkdir recombine
$ mv proteins.dat recombine/
$ cp recombine/proteins.dat ../proteins-saved.dat
$ ls
~~~
>
> 1. `proteins-saved.dat recombine`
> 2. `recombine`
> 3. `proteins.dat recombine`
> 4. `proteins-saved.dat`
>
{{% expand "Solution" %}}
We start in the `/home/jamie/data` directory, and create a new folder called
`recombine`.  The second line moves (`mv`) the file `proteins.dat` to the new
folder (`recombine`).  The third line makes a copy of the file we just moved.
The tricky part here is where the file was copied to.  Recall that `..` means
"go up a level", so the copied file is now in `/home/jamie`.  Notice that `..`
is interpreted with respect to the current working directory, **not** with
respect to the location of the file being copied.  So, the only thing that will
show using `ls` (in `/home/jamie/data`) is the recombine folder.

1. No, see explanation above.  `proteins-saved.dat` is located at `/home/jamie`
2. Yes
3. No, see explanation above.  `proteins.dat` is located at
   `/home/jamie/data/recombine`
4. No, see explanation above.  `proteins-saved.dat` is located at `/home/jamie`
{{% /expand %}}
>

<br>

> *Challenge*: Organizing Directories and Files
> ---------------------------------------------
> Jamie is working on a project and she sees that her files aren't very well
> organized:
>
~~~text
$ ls

analyzed  fructose.dat    raw   sucrose.dat
~~~
>
> The `fructose.dat` and `sucrose.dat` files contain output from her data
> analysis. What command(s) covered in this lesson does she need to run so that
> the commands below will produce the output shown?
>
~~~text
$ ls

analyzed   raw
~~~
>
~~~text
$ ls analyzed

fructose.dat    sucrose.dat
~~~
>
{{%expand "Solution" %}}

~~~text
$ mv *.dat analyzed
~~~

Jamie needs to move her files `fructose.dat` and `sucrose.dat` to the `analyzed`
directory.  The shell will expand `\*.dat` to match all `.dat` files in the
current directory.  The `mv` command then moves the list of .dat files to the
"analyzed" directory.
{{% /expand %}}
>

<br>

> *Challenge*: Copy with Multiple Filenames
> -----------------------------------------
> For this exercise, you can test the commands in the `data-shell/data`
> directory.
>
> In the example below, what does `cp` do when given several filenames and a
> directory name?
>
~~~text
$ mkdir backup
$ cp amino-acids.txt animals.txt backup/
~~~
>
> In the example below, what does `cp` do when given three or more file names?
>
~~~text
$ ls

amino-acids.txt  animals.txt  backup/  elements/  morse.txt  pdb/  planets.txt
salmon.txt       sunspot.txt
~~~
>
~~~text
$ cp amino-acids.txt animals.txt morse.txt
~~~
>
{{% expand "Solution" %}}
If given more than one file name followed by a directory name (i.e. the
destination directory must be the last argument), `cp` copies the files to the
named directory.

If given three file names, `cp` throws an error because it is expecting a
directory name as the last argument.

~~~text
cp: target 'morse.txt' is not a directory
~~~
{{% /expand %}}
>

<br>

> *Challenge*: Copy A Folder Structure But Not The Files
> ------------------------------------------------------
> You're starting a new experiment, and would like to duplicate the file
> structure from your previous experiment without the data files so you can add
> new data.
>
> Assume that the file structure is in a folder called `2016-05-18-data`, which
> contains a `data` folder that in turn contains folders named `raw` and
> `processed` that contain only data files.  The goal is to copy the file
> structure of the `2016-05-18-data` folder into a folder called
> `2016-05-20-data` and remove the data files from the directory you just
> created.
>
> Which of the following set of commands would achieve this objective?  What
> would the other commands do?
>
~~~text
$ cp -r 2016-05-18-data/ 2016-05-20-data/
$ rm 2016-05-20-data/raw/*
$ rm 2016-05-20-data/processed/*
~~~
>
~~~text
$ rm 2016-05-20-data/raw/*
$ rm 2016-05-20-data/processed/*
$ cp -r 2016-05-18-data/ 2016-5-20-data/
~~~
>
~~~text
$ cp -r 2016-05-18-data/ 2016-05-20-data/
$ rm -r -i 2016-05-20-data/
~~~
>
{{% expand "Solution" %}}

The first set of commands achieves this objective.  First we have a recursive
copy of a data folder.  Then two `rm` commands which remove all files in the
specified directories.  The shell expands the `*` wild card to match all files
and subdirectories.

The second set of commands have the wrong order: attempting to delete files
which haven't yet been copied, followed by the recursive copy command which
would copy them.

The third set of commands would achieve the objective, but in a time-consuming
way: the first command copies the directory recursively, but the second command
deletes interactively, prompting for confirmation for each file and directory.
{{% /expand %}}
>

Key Points
---------
- `cp old new` copies a file

- `mkdir path` creates a new directory

- `mv old new` moves (renames) a file or directory

- `rm path` removes (deletes) a file."

- The shell does not have a trash bin: once something is deleted, it's really
  gone.

---

*Gabriel Devenyi, Christina Koch, and Ashwin Srinath (eds): "Software
Carpentry: The Unix Shell." Version 2016.06, June 2016,
https://github.com/swcarpentry/shell-novice*
