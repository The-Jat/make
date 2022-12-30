## What is Makefile
When your code is separated into many several files that have interdependencies, it is natural to look for an automated way of compiling your program,
because compilation and linking become very complicated. The make program
was designed to help developers automatically build executable programs.
Once you have set up a Makefile that describes the components of your
program, their relationships, and how to build the various components, then
make will do the build for you correctly every time.

## Why use make?
There are two main reasons to use make.
1. Simpler compilation and linking
make allows a shorthand for complicated commands or a large sequence of
commands.
Explicitly typing clang++ -Wall -Wextra -std=c++11 -o foo bar.cpp
baz.cpp for each compilation quickly becomes cumbersome. When you
have a Makefile properly configured, the foo executable could instead be
compiled by typing make foo.

2. Faster re-compilation
Another advantage of make is that it only recompiles code that needs to be
recompiled. This is particularly useful in large programs with 300+ files.
If you change only one of then, you need not recompile everything: make
compiles the files you changed and anything that depends on it.
Compiling C++ code is a multistep process
Running the command clang++ -o foo bar.cpp baz.cpp will follow the
steps in Figure 1 to make bar.o baz.o, and will combine the .o files into
an executable named foo. By default, most compilers delete the intermediate
files (.cpp .s .o) after creating the executable. Which means that every
.cpp file must always recompiled. If a .cpp file hasn’t been changed since
the last compilation, recompiling it is wasteful since its previous .o file
could be reused. As projects get larger, recompiling all sources files for each
compilation can become very slow.
make automatically tracks which components of an executable have changed
since the last time the executable was compiled. We typically write
Makefiles to save .o files. That way, compiling an executable only requires
remaking .o files that are not up to date, and combining them with the old
.o files.

## Anatomy of a Makefile

> Makefile rules

Makefile rules are the building blocks of Makefiles. They describe an
action to perform when the rule is evoked, and also when to perform that
action.
>target: prerequisites...
&nbsp;&nbsp;&nbsp;&nbsp;recipe

A Makefile rule is made up of :-
&nbsp;&nbsp;&nbsp;&nbsp;• A target, which is the argument given to make on the commandline
(i.e make target). The target usually is the name of the file that will
be created after the rule is executed, but it can also be the name of
an action to carry out (clean, install, etc. . . ).
&nbsp;&nbsp;&nbsp;&nbsp;• A list of 0 or more prerequisites, which are files or targets that
the current target depends on.
&nbsp;&nbsp;&nbsp;&nbsp;• A recipe, which is the shell command(s) executed by the Makefile
rule.

Make will execute the recipe if a file named target does not exist, or if
any of the prerequisites are more recent than target.

Example:
```
bar.o: bar.cpp bar_header.h
    clang++ -c bar.cpp
```
>• bar.o is the target
• bar.cpp bar_header.h are the prerequisites
• clang++ -c bar.cpp is the recipe

>Important: When compiling code, we only compile .cpp files, not
.h files

When you type make bar.o into the console, the first thing that make will
do is check the timestamp of bar.o and all of the files it depends (bar.cpp
and bar_header.h in this example). Then it will run the recipe (in this
case clang++ -c bar.cpp) if bar.o doesn’t exist, or if either bar.o or
bar_header.h is more recent than bar.o.




