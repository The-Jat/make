## Special Symbols
There are a bunch of fancy things you can do with Make using wildcard and expanded symbols. Given the following snippet, here are a couple that might come in handy.
```
target1: dependency1 dependency2
	command1
	command2
```
$@ expands to the target name, i.e. target1
$< expands to the first dependency, i.e. dependency1
$^ expands to the complete list of dependencies, i.e. dependency1 dependency2
You can use the wildcard operator, %, to apply a rule to multiple files. For example, the following rule compiles all .cpp files in the directory to correspondingly named .o files:
```
%.o: %.cpp
	g++ -Wall -c $< -o $@ 
```
