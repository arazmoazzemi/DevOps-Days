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



##### **Change input vlaues to string with _**<$*>**_**


##### **Change input Values to string with _**<$@>**_**


##### **Exit Code with _**$?**_**


