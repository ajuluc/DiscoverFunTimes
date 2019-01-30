# Loading modules

> *Notation: lines beginning with a `$` you should enter at the terminal, which typically ends with a `$` (but don't enter an additional `$`).*

The research computing staff maintain a lot of software on discovery,
but it is not all compatible with each other (there are different versions
  of the same software, for example) so it is not all available
all of the time by default - you have to choose which you want to load.
These are organized in modules.

List the available modules:

    $ module avail

As you can see, there are a lot, including quantum chemistry packages,
molecular dynamics packages, specialized compilers, matlab, etc.
See for example there are three versions of python:

    python/2.7.15
    python/3.6.6
    python/3.7.0
    python/3.7.1

You probably want the last one, but find out more about it by typing:

    $ module whatis python/3.7.1

This will tell you about it, and crucially, a list of the prerequisites, if there are any.
These contain compilers and libraries that the software you want was compiled against, and
are needed for it to run.
For example, try:

    $ module whatis python/3.7.0

it will tell you that, if you wanted to use pytorch you would need to load the module `openmpi/3.1.1`
*before* loading the module `python/3.7.0`.

But before you do anything, let's see what python you will get without loading the modules.
There may be several programs called
`python` and when you type `python` the computer has to pick one of them to run.
The way it does this is by searching through all the directories listed in your `$PATH` until it finds one containing
an executable called `python`, and runs that.
I can see my current `$PATH` by typing `echo $PATH`:

    $ echo $PATH
    /shared/centos7/discovery/bin:/usr/lib64/qt-3.3/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/ajulu.c/.local/bin:/home/ajulu.c/bin

The `which` program is a helpful command that tells you which executable program will
be run when you ask for a given program. ie. which is the first directory in your `$PATH`
that contains an executable with the requested name. For example:

    $ which python
    /usr/bin/python

To see what version this is:

    $ python -V
    Python 2.7.5

Let's see if there's a `python3` program:

    $ which python3
    /usr/bin/which: no python3 in (/shared/centos7/discovery/bin:/usr/lib64/qt-3.3/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/ajulu.c/.local/bin:/home/ajulu.c/bin)

This is telling us that there is no executable called `python3` in any of the directories listed in the `$PATH`. If I were to try executing it, it would fail:

    $ python3
    -bash: python3: command not found

Now let's load the modules we found out about earlier:

    $ module load python/3.7.1

Or (if you wanted 3.7.0 with pytorch) with the pre-requisites:

    $ module load openmpi/3.1.1 python/3.7.0

And try again:

    $ which python
    /usr/bin/python

That is the same as before!:

    $ python -V
    Python 2.7.5

But now we have a new program called `python3` available, which wasn't before:

    $ which python3
    /shared/centos7/python/3.7.1/bin/python3
    $ python3 -V
    Python 3.7.1

Now we can execute it, type some python commands, and get the results.
Press control-D to quit it when you're done:

    $ python3
    Python 3.7.1 (default, Nov 14 2018, 15:27:21) 
    [GCC 4.8.5 20150623 (Red Hat 4.8.5-28)] on linux
    Type "help", "copyright", "credits" or "license" for more information.
    >>> print("Hello, World!")
    Hello, World!
    >>>

You learned in section 7 of the UNIX tutorial
[how to compile UNIX software packages](http://www.ee.surrey.ac.uk/Teaching/Unix/unix7.html)
but if you want some new software installed, it's often easiest to ask the friendly folks at
researchcomputing@northeastern.edu to install it for you as a new module, rather than trying
to configure and compile it yourself. Especially if you think it'll be useful for other people.

When loading a new module remember to always use `module whatis` to find out what the
prerequisites are.  If you want to run several programs at the same time, and aren't sure
what order to load the combined list of prerequisites in, try a few sensible combinations
then ask researchcomputing@northeastern.edu for help!

---
Next: [3. Editing your .bashrc](03-bashrc.md)
