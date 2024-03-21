# Bahs Script

__Example of ($ and Input) variables__

```
touch test.sh
```
```bash
#! ---> shebang for communicate with interpreters
chmod +x ---> execute permission
```
```
touch test.sh
chmod +x test.sh
```

---
### a-z A-Z 0-9 _
## Imprtant : Variables should not start with a number.

### In Bash, you can name variables using your desired names; however, there are certain conditions and constraints for variable naming. Here are some of these conditions:

### Variable names must start with a letter or underscore (_).
### Variable names can only contain uppercase and lowercase English letters, digits, and underscores (_).
#### Variable names are case-sensitive. In other words, variables named "Var" and "var" are considered different.
### Variable names should not conflict with Bash keywords. For example, names like "if" or "while" are not allowed.
### It's recommended to avoid using uppercase letters in variable names since system variables are typically named in uppercase, which might lead to conflicts.
### In general, it's advisable to name variables in Bash in a logical and understandable manner, avoiding conflicts with other names.
---

```bash
#!/usr/bin/bash
CLASS="Hello DevOps!"
echo $CLASS
```

### Readonly:
```bash
#!/usr/bin/bash

CLASS="Hello Devops!"

readonly CLASS

echo $CLASS

CLASS="DevOps"

echo $CLASS

```
### Command set -e:
## Non-zero exit status

```bash 
#!/usr/bin/bash

set -e

CLASS="Hello Devops!"

readonly CLASS

echo $CLASS


CLASS="DevOps"

echo $CLASS

```
UNSET vlaues:
```
#!/usr/bin/bash

set -e

CLASS="Hello Devops!"

unset CLASS

echo $CLASS

```

---
### Env variables , Local variables, Shell variables:
---
---

## Passing variables from one process to child processes

```bash
touch test.sh
```
```bash
#!/usr/bin/bash

export CLASS="Hello DevOps!"

echo $CLASS

python3 test.py
```
```bash
touch test.py
```
```python

#!/usr/bin/python3

from os import environ

print(environ.get("CLASS", "NONE"))
```
### Call process:
```bash
./test.sh
```

---
---
### Special variables in bash:

Special Variable	Description
#### $0	Gets the name of the current script.
#### $#	Gets the number of arguments passed while executing the bash script.
#### $*	Gives you a string containing every command-line argument.
#### $@	It stores the list of every command-line argument as an array.
#### $1-$9	Stores the first 9 arguments.
#### $?	Gets the status of the last command or the most recently executed process.
#### $!	Shows the process ID of the last background command.
#### $$	Gets the process ID of the current shell.
#### $-	It will print the current set of options in your current shell.
---
## Example:
```
touch test.sh
```
```
#!/usr/bin/bash

which docker &>  /dev/null

if [[ $? -eq 0 ]]; then
    echo "Docker cli is installed."
els
    echo "Docker cli is not installed. "
fi
```

### Define arrays:
```
touch test.sh
```
```
#!/usr/bin/bash

NAMES=(ARAZ AREZOU ROSA)

echo $NAMES
echo ${NAMES[1]}
echo ${NAMES[2]}

NAMES[2]="CHANGED"
echo ${NAMES[2]}

```
```
#!/usr/bin/bash

NAMES=(ARAZ AREZOU ROSA)

echo ${#NAMES[@]}

```
```
#!/usr/bin/bash

IPS=($(hostname -i))

echo ${IPS[1a]}


```





