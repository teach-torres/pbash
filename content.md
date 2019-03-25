# Content
## My first Program

You should be in your home directory, which you can find in the variable $HOME:
```terminal
$ echo "$HOME"
```

You can find the current directory with either the pwd command or the PWD variable:
```terminal
pwd
$ echo "$PWD"
```
If you are not in your home directory, you can get there by typing cd and pressing Enter at the shell
prompt.

The code is nothing more than this:
```terminal
$ echo Hello, World!
```
There are three words on this command line: the command itself and two arguments. The command, 
echo, prints its arguments separated by a single space and terminated with a newline.

Before you turn that code into a script, you need to make two decisions: what you will call the file and where 
you will put it. The name should be unique (that is, it should not conflict with any other commands), and 
you should put it where the shell can find it.

Beginners often make the mistake of calling a trial script test. To see why that is bad, enter the following at
the command prompt:
```terminal
type test
```
The type command tells you what the shell will execute (and where it can be found if it is an external 
file) for any given command. In bash, type -a test will display all the commands that match the
name test:
```terminal
$ type test
test is a shell builtin
$ type -a test
test is a shell builtin
test is /usr/bin/test
```
As you can see, a command called test already exists; it is used to test file types and to compare values.

Typically, Unix command names are as short as possible. They are often the first two consonants of
a descriptive word (for example, mv for move or ls for list) or the first letters of a descriptive phrase
(for example, ps for process status or sed for stream editor).

For this exercise, call the script hw. Many shell programmers add a suffix, such as .sh, to indicate that 
the program is a shell script. The script doesn’t need it, and I use one only for programs that are being 
developed. My suffix is -sh, and when the program is finished, I remove it. A shell script becomes another 
command and doesn’t need to be distinguished from any other type of command. 

When the shell is given the name of a command to execute, it looks for that name in the directories listed
in the PATH variable. This variable contains a colon-separated list of directories that contain executable
commands. This is a typical value for $PATH:
```terminal
/bin:/usr/bin:/usr/local/bin:/usr/games
```
If your program is not in one of the PATH directories, you must give a pathname, either absolute or
relative, for bash to find it. An absolute pathname gives the location from the root of the filesystem, such as
/home/chris/bin/hw; a relative pathname is given in relation to the current working directory (which should
currently be your home directory), as in bin/hw.

Commands are usually stored in directories named bin, and a user’s personal programs are stored in a
bin subdirectory in the $HOME directory. To create that directory, use this command:
```terminal
mkdir bin
```
Now that it exists, it must be added to the PATH variable:
```terminal
PATH=$PATH:$HOME/bin
```
