Become Familiar with Shell Variables

Variables in the shell are like variables in programming. Linux contains built in variables such as:
> echo $SHELL
OUTPUT
> /bin/bash

Shell variables are typically written in uppercase and separated with '_'
e.g.
MY_VARIABLE="This is my variable"

View available variables:
> env

A variable cannot contain spaces
Values are often surrounded in double quotes or single quotes to avoid shell expansion of the values.

Variables set only exist in the current shell

Export a variable for other shell sessions:
> $OPEN_SOURCE="persists!"
> export OPEN_SOURCE
(No $ needed)

Type bash and enter to start a new shell, the variable will appear in env and be usable

Remove a variable:
> unset VARIABLE_NAME
(No $ needed)


