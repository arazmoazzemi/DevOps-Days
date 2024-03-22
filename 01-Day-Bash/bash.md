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

echo ${IPS[1]}


```

Input values:

```
#!/usr/bin/bash

read -p "Input A:" A

read -p "Input B:" B

RESULT=`expr $A + $B`

echo $RESULT

```

### Using expr Command:
```
# Addition
result=$(expr 5 + 3)
echo $result   # Output: 8

# Subtraction
result=$(expr 10 - 4)
echo $result   # Output: 6

# Multiplication
result=$(expr 6 \* 7)   # Note: * needs to be escaped or quoted
echo $result   # Output: 42

# Division
result=$(expr 20 / 4)
echo $result   # Output: 5
```

### Using Arithmetic Expansion:
```
# Addition
result=$((5 + 3))
echo $result   # Output: 8

# Subtraction
result=$((10 - 4))
echo $result   # Output: 6

# Multiplication
result=$((6 * 7))
echo $result   # Output: 42

# Division
result=$((20 / 4))
echo $result   # Output: 5

# Modulus (Remainder)
result=$((20 % 3))
echo $result   # Output: 2

# Exponentiation
result=$((2 ** 3))
echo $result   # Output: 8
```
```
#!/usr/bin/bash

read -p "Input A: " A

let A++
# let A=A+10

echo $A
```

### In Bash, there are six relational operators for number comparison:

#### Equal to (-eq): Checks if two numbers are equal.

```bash
if [ "$num1" -eq "$num2" ]; then
    echo "$num1 is equal to $num2"
fi
```


#### Not equal to (-ne): Checks if two numbers are not equal.

```bash
if [ "$num1" -ne "$num2" ]; then
    echo "$num1 is not equal to $num2"
fi
```

#### Greater than (-gt): Checks if the first number is greater than the second number.

```bash
if [ "$num1" -gt "$num2" ]; then
    echo "$num1 is greater than $num2"
fi
```

#### Greater than or equal to (-ge): Checks if the first number is greater than or equal to the second number.

```bash
if [ "$num1" -ge "$num2" ]; then
    echo "$num1 is greater than or equal to $num2"
fi
```

#### Less than (-lt): Checks if the first number is less than the second number.

```bash
if [ "$num1" -lt "$num2" ]; then
    echo "$num1 is less than $num2"
fi
```

#### Less than or equal to (-le): Checks if the first number is less than or equal to the second number.

```bash
if [ "$num1" -le "$num2" ]; then
    echo "$num1 is less than or equal to $num2"
fi
```

### Logical Operators:
#### Logical AND (&&): Executes the next command if the previous command succeeded.
#### Logical OR (||): Executes the next command if the previous command failed.
#### Logical NOT (!): Inverts the result of the following condition.

### AND (&&):
```bash
[ -f file.txt ] && echo "File exists"
```

### OR (||):
```bash
[ -d directory ] || echo "Directory does not exist"
```

### NOT (!):
```bash
! [ -f file.txt ] && echo "File does not exist"
```

### Check, Is the string empty:
```bash
#!/usr/bin/bash

A=''

[[ -z $A ]]

echo $?
```


