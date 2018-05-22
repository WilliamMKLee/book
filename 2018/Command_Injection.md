# Command Injection

refer [命令注入攻擊](https://www.owasp.org/index.php/Command_Injection)

```c
#include <stdio.h>
#include <unistd.h>

int main(int argc, char **argv) {
    char cat[] = "cat ";
    char *command;
    size_t commandLength;

    commandLength = strlen(cat) + strlen(argv[1]) + 1;
    command = (char *) malloc(commandLength);
    strncpy(command, cat, commandLength);
    strncat(command, argv[1], (commandLength - strlen(cat)) );

    system(command);
    return (0);
}
```

Used normally, the output is simply the contents of the file requested:

```
$ ./catWrapper Story.txt
When last we left our heroes...
```

However, if we add a semicolon and another command to the end of this line, the command is executed by catWrapper with no complaint:

```
$ ./catWrapper "Story.txt; ls"
When last we left our heroes...
Story.txt               doubFree.c              nullpointer.c
unstosig.c              www*                    a.out*
format.c                strlen.c                useFree*
catWrapper*             misnull.c               strlength.c             useFree.c
commandinjection.c      nodefault.c             trunc.c                 writeWhatWhere.c
```

If catWrapper had been set to have a higher privilege level than the standard user, arbitrary commands could be executed with that higher privilege.


## Example

自己實做一次; 其實看起來就像 SQL injection; 在做 query 或是 執行時未把 command 做適當處理(如 escape 特殊字元)導致使用者可以做一些攻擊


```py
"""
cat the file context
./cli_cat.py <file_path>
"""
import os
from sys import argv
cmd = argv[1]
os.system('cat ' + cmd)
```

Used normally

```shell
# create a text file
echo "hello" > hello.txt


python cli_cat.py "hello.txt"
hello
python cli_cat.py hello.txt
hello
```

Inject

```shell
python cli_cat.py "hello.txt; ls"
hello
cli_cat.py  hello.txt  mytmp 
```

How to prevent it

escape `'`, `"` and '\'


```py
"""
cat the file context
./cli_cat.py <file_path>
"""
import os
from sys import argv
import re

cmd = re.escape(argv[1])
os.system('cat ' + cmd)
```

執行

```shell
python cli_cat.py "hello.txt; ls"
cat: 'hello.txt; ls': No such file or directory
```
