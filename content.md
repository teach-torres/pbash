

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
For this change to be applied to every shell you open, add it to a file that the shell will source when it is
invoked. This will be .bash_profile, .bashrc, or .profile depending on how bash is invoked. These files
are sourced only for interactive shells, not for scripts.

### Creating the File and Running the Script
Usually you would use a text editor to create your program, but for a simple script like this, it’s not necessary
to call up an editor. You can create the file from the command line using redirection:

```terminal
echo echo Hello, World! > bin/hw
```

The greater-than sign (>) tells the shell to send the output of a command to the specified file, rather than
to the terminal. 

The program can now be run by calling it as an argument to the shell command:

```terminal
bash bin/hw
```

That works, but it’s not entirely satisfactory. You want to be able to type hw, without having to precede it
with bash, and have the command executed. To do that, give the file execute permissions:

```terminal
chmod +x bin/hw
```

Now the command can be run using just its name:

```terminal
$ hw
Hello, World!
```

### Source command

. (a period) is a bash shell built-in command that executes the commands from a file passed as argument, 
in the current shell. 'source' is a synonym for '.'.

source command executes the provided script (executable permission is not mandatory) in the current 
shell environment, while ./ executes the provided executable script in a new shell.

source command do have a synonym . filename.

>> To make it more clear, have a look at the following script, which sets the alias.

make_alias

```terminal
#! /bin/bash
alias myproject='cd ~/Documents/Projects/2015/NewProject'
```

Now we have two choices to execute this script. But with only one option, the desired alias for 
current shell can be created among these two options.

**Option 1: ./make_alias**

Make script executable first.
```terminal
chmod +x make_alias
```
Execute
```terminal
./make_alias
```

Verify
```terminal
alias
```
Output
```terminal
**nothing**
```
Whoops! Alias is gone with the new shell.

Let's go with the second option.

**Option 2: source make_alias**
Execute
```terminal
source make_alias
```
or
```terminal
. make_alias
```
Verify
```terminal
alias
```
Output
```terminal
alias myproject='cd ~/Documents/Projects/2015/NewProject'
```
Yeah Alias is set.

### TExt Editor

**Note** In Windows text files, !” lines end with two characters: a carriage return (CR) and a linefeed (LF).
On Unix systems, such as Linux, lines end with a single linefeed. If you write your programs in a Windows text
editor, you must either save your files with Unix line endings or remove the carriage returns afterward.

### Building a Better “Hello, World!”

Earlier in the chapter you created a script using redirection. That script was, to say the least, minimalist.
All programs, even a one liner, require documentation. Information should include at least the author, the
date, and a description of the command. Open the file bin/hw in your text editor, and add the information in
Listing 1-1 using comments.

Listing 1-1. hw
```
#!/bin/bash
#: Title : hw
#: Date : 2008-11-26
#: Author : "Chris F.A. Johnson" <shell@cfajohnson.com>
#: Version : 1.0
#: Description : print Hello, World!
#: Options : None

printf "%s\n" "Hello, World!" !"
```
Comments begin with an octothorpe, or hash, at the beginning of a word and continue until the end of
the line. The shell ignores them. I often add a character after the hash to indicate the type of comment. I can
then search the file for the type I want, ignoring other comments.
The first line is a special type of comment called a shebang or hash-bang. It tells the system which
interpreter to use to execute the file. The characters #! must appear at the very beginning of the first line; in
other words, they must be the first two bytes of the file for it to be recognized.
