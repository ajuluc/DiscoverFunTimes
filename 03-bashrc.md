# Editing your .bashrc file

If there are some things you wish to do every time you log in to
the computer, such as load your required modules, configure
your terminal, or set some environment variables, then it
saves time to put them in a file that the `bash` shell will
run every time it starts. This is your `.bashrc` file, in your home
directory. It probably exists already (with some default contents)
but doesn't show up when you type `ls` because its name begins with
a `.` so it is hidden. To look for it, try:

    $ cd ~
    $ ls -al

To print its contents:

    $ cat .bashrc

To edit it, using the `vi` ext editor [(some instructions here)](https://www.cs.colostate.edu/helpdocs/vi.html):

    $ vi .bashrc

You want to add these commands, for `python3`:

    module load python/3.7.1

To add the     `module load python/3.7.1 command` to your `vi` visual editor in UNIX, use the following commands to navigate the page:
`:` using this sends the cursor to the bottom of the screen. This command is completed by hitting the <Return> or Enter key
`h` or Backspace to move the cursor left one character
`l` or spacebar to move the cursor right one character
`k` or arrow up <^> to move the cursor up one line 
`j` or <return> to move the cursor down one line 
	
To insert text before the cursor:
`i` then hit <esc> to get out of the insert mode

After adding the `module load python/3.7.1 command` use the following commands to save to save and exit 
`:w` to save then `:q` to exit. You can also combine both save and exit into one by using this command `:wq`




So that your `.bashrc` file looks something like:

```bash
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
	. /etc/bashrc
fi

module load python/3.7.1
```

**Remember!** Your `.bashrc` is only executed when you first log in to a computer,
so to test the effect of editing your `.bashrc` file you must log out and log
back in again.   (You can type `source .bashrc` to load an updated file, but
this will do it *on top of* the original file, and the effect may be unexpected.
It is safest to always log out and in again.)

Log out like this:

    $ logout

---
Next: [4. Installing additional Python packages](04-python-packages.md)
