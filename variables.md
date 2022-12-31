## Makefile variables
Variables can be defined in Makefile to make them more configurable
Variables are declared as:
```
varName = value
```
The value of a variable can then be accessed by wrapping the variable in
```
${} or $():
${varName} or $(varName)
```

Makefile variables can be used to specify the compiler, and any compilation settings.
• CXX is the name of the C++ compiler
• CXXFLAGS are the compiler options for compiling .cpp files into .o files
(It’s possible to also see CC and CFLAGS which are the C equivalents for CXX
and CXXFLAGS).

## Why Variables.

When you start to write more complicated Makefiles, you’ll find yourself frequently repeating commands and arguments. In order to alleviate this, Makefile offers variables. Here’s an example Makefile where we’ve abstracted most of the g++ calls into variables.

```
COMPILER=g++
OPTIONS=-g -std=c++17 -pedantic -Wall -Wextra -Werror -Wshadow -Wconversion -Wunreachable-code
COMPILE=$(COMPILER) $(OPTIONS)

program: main.cpp
	$(COMPILE) main.cpp -o program
```
