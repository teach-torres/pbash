<!-- MarkdownTOC -->

- [1. My first Program](#1-My-first-program)
- [2. Input, Output, and Throughput](#2-Input,-Output,-and-Throughput)
  * [2.1 Differential Identities](#11-differential-identities)
  * [2.2 Deriving Matrix Derivatives](#12-deriving-matrix-derivatives)
    + [2.2.1 Abstract examples: repeat identities 1](#121-abstract-examples-repeat-identities-1)
    + [2.2.2 Actual examples: assisted by identities 2](#122-actual-examples-assisted-by-identities-2)
- [3. Conclusion](#2-conclusion)

<!-- Como crear la tabla de contenido
<!-- https://github.com/LynnHo/Matrix-Calculus/blob/master/README.md -->
<!-- /MarkdownTOC -->

## 1. My first Program

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

printf "%s\n" "Hello, World!"
```
Comments begin with an octothorpe, or hash, at the beginning of a word and continue until the end of
the line. The shell ignores them. I often add a character after the hash to indicate the type of comment. I can
then search the file for the type I want, ignoring other comments.
The first line is a special type of comment called a shebang or hash-bang. It tells the system which
interpreter to use to execute the file. The characters #! must appear at the very beginning of the first line; in
other words, they must be the first two bytes of the file for it to be recognized.

### Summary
The following are the commands, concepts, and variables you learned in this chapter.

#### Commands

• pwd: Prints the name of the current working directory

• cd: Changes the shell’s working directory

• echo: Prints its arguments separated by a space and terminated by a newline

• type: Displays information about a command

• mkdir: Creates a new directory

• chmod: Modifies the permissions of a file

• source: a.k.a. . (dot): executes a script in the current shell environment

• printf: Prints the arguments as specified by a format string

#### Concepts

• Script: This is a file containing commands to be executed by the shell.

• Word: A word is a sequence of characters considered to be a single unit by the shell.

• Output redirection: You can send the output of a command to a file rather than the
terminal using > FILENAME.

• Variables: These are names that store values.

• Comments: These consist of an unquoted word beginning with #. All remaining
characters on that line constitute a comment and will be ignored.

• Shebang or hash-bang: This is a hash and an exclamation mark (#!) followed by the
path to the interpreter that should execute the file.

• Interpreter: This is a program that reads a file and executes the statements it contains.
It may be a shell or another language interpreter such as awk or python.

#### Concepts

• Script: This is a file containing commands to be executed by the shell.

• Word: A word is a sequence of characters considered to be a single unit by the shell.

• Output redirection: You can send the output of a command to a file rather than the
terminal using > FILENAME.

• Variables: These are names that store values.

• Comments: These consist of an unquoted word beginning with #. All remaining
characters on that line constitute a comment and will be ignored.

• Shebang or hash-bang: This is a hash and an exclamation mark (#!) followed by the
path to the interpreter that should execute the file.

• Interpreter: This is a program that reads a file and executes the statements it contains.
It may be a shell or another language interpreter such as awk or python.

### Exercises

1. Write a script that creates a directory called bpl inside $HOME. Populate this
directory with two subdirectories, bin and scripts.

2. Write a script to create the “Hello, World!” script, hw, in $HOME/bpl/bin/; make it
executable; and then execute it.

page 9/237

## 2. Input, Output, and Throughput

Two of the commands we used in chapter 1 are workhorses of the shell scripter’s stable: echo and printf.
Both are bash builtin commands. Both print information to the standard output stream, but printf is much
more powerful, and echo has its problems. 

In this chapter, I’ll cover echo and its problems, the capabilities of printf, the read command, and the
standard input and output streams. I’ll start, however, with an overview of parameters and variables.

### Parameter and Variables

To quote the bash manual (type man bash at the command prompt to read it), “A parameter is an entity that
stores values.” There are three types of parameters: positional parameters, special parameters, and variables.
Positional parameters are arguments present on the command line, and they are referenced by a number.
Special parameters are set by the shell to store information about aspects of its current state, such as the
number of arguments and the exit code of the last command. Their names are nonalphanumeric characters
(for example, *, #, and _). Variables are identified by a name. What’s in a name? I’ll explain that in the
“Variables” section.

The value of a parameter is accessed by preceding its name, number, or character with a dollar sign, as
in $3, $#, or $HOME. The name may be surrounded by braces, as in ${10}, ${PWD}, or ${USER}.

Positional Parameters

The arguments on the command line are available to a shell program as numbered parameters. The first
argument is $1, the second is $2, and so on.

You can make the hw script from chapter 1 more flexible by using a positional parameter. Listing 2-1
calls it hello.

Listing 2-1. hello
```
#: Description: print Hello and the first command-line argument
printf "Hello, %s!\n" "$1"
```

Now you can call the script with an argument to change its output:
```
$ hello John
Hello, John!
$ hello Susan
Hello, Susan!
```

The Bourne shell could only address up to nine positional parameters. If a script used $10, it would be
interpreted as $1 followed by a zero. To be able to run old scripts, bash maintains that behavior. To access
positional parameters greater than 9, the number must be enclosed in braces: ${15}.

The script is passed to the parameters that can be accessed via their positions, $0, $1, $2 and so on.
The function shift N moves the positional parameters by N positions, if you ran shift (the default value of
N is 1), then $0 would be discarded, $1 would become $0, $2 would become $1, and so on: they would all be
shifted by 1 position. There are some very clever and simple uses of shift to iterate through a list of paramters
of unknown length.

**Note** The shift function is distructive: that is, the paramters discarded are gone and cannot be
retrieved again.
