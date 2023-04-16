# Bash Scripting

Every bash script is an executable file that runs tasks. Most often shell scripts
are used to automate routine tasks. 

Every shell script starts with the Shebang ``#!`` \
If you are using the Bash shell the Shebang would be ``#!/bin/bash`` \
Now "/bin" is no longer an ordinary directory. It is therefore recommended
to use the following Shebang since it sources your environment and will point you
to the correct Bash shell.

**#!/usr/bin/env bash**


It's a good practice but not mandatory to use the **.sh** extension for shell script files.

## Helpful Tools

### Test command
The test command is useful since it can test the properties of files, values of integers,
properties of files, etc. Test can be used for if, then, else statements.

Here is a simple bash script using the test command.

````
#!/bin/bash

if test $1 -eq 500 
then
        echo "You picked the right number!"
else
        echo "You failed!"
fi
````
You can also put the if statement into brackets. The square brackets are the same as the test command.
````
#!/bin/bash

if [ $1 -eq 500 ]
then
        echo "You picked the right number!"
else
        echo "You failed!"
fi
````
### Script Debug Mode

``bash -x mygreatscript.sh`` Shows you the script in debug mode.
