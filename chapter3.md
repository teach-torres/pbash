## Looping and Branching

At the heart of any programming language are iteration and conditional execution. Iteration is the repetition
of a section of code until a condition changes. Conditional execution is making a choice between two or
more actions (one of which may be to do nothing) based on a condition.

In the shell, there are three types of loop (while, until, and for) and three types of conditional
execution (if, case, and the conditional operators && and ||, which mean AND and OR, respectively). With the
exception of for and case, the exit status of a command controls the behavior.

### Exit Status

You can test the success of a command directly using the shell keywords while, until, and if or with the
control operators && and ||. The exit code is stored in the special parameter $?.

If the command executed successfully (or true), the value of $? is zero. If the command failed for some
reason, $? will contain a positive integer between 1 and 255, inclusive. A failed command usually returns 1.
Zero and non-zero exit codes are also known as true and false, respectively.

A command may fail because of a syntax error:
