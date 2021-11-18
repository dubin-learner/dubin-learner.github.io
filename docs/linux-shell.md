# Linux Shell基础

本文将总结一些Linux Shell的相关知识，以及在工作中用过的使用技巧。

社区翻译的《The Linux Command》中文版[网址](http://billie66.github.io/TLCL/)，可以在线阅读或下载pdf，是一本不错的参考书。

## shell脚本第一行：#!/bin/bash的含义
直接说结论：第一行的内容指定了该脚本使用的解释器的路径，比如通过`#!/bin/python`来指定python解释器执行该脚本。

这个指定路径只能放在文件的第一行。如果第一行写错或者不写，系统会有一个默认的解释器进行解释。对于Ubuntu系统，通常就是`/bin/bash`。
## Linux Shell不同方法执行脚本的区别
一般Linux上执行一个脚本，有如下几种方法：
```bash
bash test.sh
sh test.sh
source test.sh
. test.sh
./test.sh
```
**注意**：可以通过type来查看命令类型，通过help来查看命令介绍。以source为例：
```bash
$ type source
source is a shell builtin
$ help source
source: source filename [arguments]
    Execute commands from a file in the current shell.

    Read and execute commands from FILENAME in the current shell.  The
    entries in $PATH are used to find the directory containing FILENAME.
    If any ARGUMENTS are supplied, they become the positional parameters
    when FILENAME is executed.

    Exit Status:
    Returns the status of the last command executed in FILENAME; fails if
    FILENAME cannot be read.
```
测试脚本：
```bash
#!/bin/bash
echo "Print Bash Path:$SHELL"
echo $EXPORT_VAR
echo $LOCAL_VAR
TEST_SET=yes
```
提前设置`EXPORT_VAR`、`LOCAL_VAR`和`TEST_SET`这几个变量：
```bash
export EXPORT_VAR=export
LOCAL_VAR=local
TEST_SET=no
```
### source和.
这两个命令等价。都是从将当前进程作为父进程，创建子进程执行脚本的内容。子进程会继承所有当前shell的环境变量。该脚本可以**无**执行权限。

source作用于当前的bash环境，即在子进程中定义的变量，执行脚本后在父进程中仍然存在。

在设置变量之后，通过source或.运行脚本：
```bash
$ source test.sh
Print Bash Path:/bin/bash
export
local
$ echo $TEST_SET
yes
```
可以看到，子进程继承了所有的变量（无论是否export），并且修改的`TEST_SET`在脚本运行结束后同步到了当前的shell中。
### sh和bash
bash是sh的增强版本，提供了更多的功能。在ubuntu中sh只是bash的一个链接。将当前进程作为父进程，创建子进程执行脚本的内容。该脚本可以**无**执行权限。

用同样的流程和测试脚本，通过bash运行：
```bash
$ bash test.sh
Print Bash Path:/bin/bash
export

$ echo $TEST_SET
no
```
可以看到，通过这种方式运行的脚本，在子进程中仅继承了export方式定义的变量；并且修改`TEST_SET`后并不影响当前shell中`TEST_SET`的值。
### ./
执行脚本，与bash类似，创建子进程执行脚本内容，但要求该脚本**有**执行权限。

还是通过相同的流程进行测试：
```bash
$ ./test.sh
-bash: ./test.sh: Permission denied
$ chmod +x test.sh
$ ./test.sh
Print Bash Path:/bin/bash
export

$ echo $TEST_SET
no
```
可以看到，除了需要给脚本添加上执行权限之外，结果和通过bash运行脚本相同。
## Linux连续执行多条命令

有几种方式：分号`;`、与`&&`、或`||`，分别对应不同的使用场景。

### 分号`;`
使用分号对多条命令进行间隔，相当于将命令分隔在不同的行。无论上一条命令执行成功与否，执行完成后都要执行下一条命令。
```bash
$ echo 1; echoo 2; echo 3; echo 4
1
Command 'echoo' not found, did you mean:
  command 'echo' from deb coreutils
Try: sudo apt install <deb name>
3
4
```
### 与`&&`
使用与操作进行间隔，根据逻辑与的特性，只有上一条命令执行成功时，才会执行下一条命令；执行失败则直接退出。
```bash
$ echo 1 && echoo 2 && echo 3 && echo 4
1
Command 'echoo' not found, did you mean:
  command 'echo' from deb coreutils
Try: sudo apt install <deb name>
```
### 或`||`
使用或操作进行间隔，格局逻辑或的特性，如果上一条命令执行成功，则直接退出；否则继续执行下一条命令，直到成功为止。
```bash
$ echo 1 || echoo 2
1
$ echoo 1 || echoo 2 || echo 3 || echo 4
Command 'echoo' not found, did you mean:
  command 'echo' from deb coreutils
Try: sudo apt install <deb name>
Command 'echoo' not found, did you mean:
  command 'echo' from deb coreutils
Try: sudo apt install <deb name>
3
```
对以上几种情况进行组合，可以控制命令执行以适应不同的需求。
## 通过cat、tail、head来查看文件中的部分内容
cat命令可以在命令行中输出文本文件的内容，用法`cat filename`。在此基础上，可以通过`head`和`next`指定要显示的一部分文本。

用法示例：
```bash
# 查看所有内容
cat filename
# 查看前100行的内容
cat filename | head -n 100
# 查看后100行的内容
cat filename | tail -n 100
# 查看从100行到结尾的内容
cat filename | tail -n +100
# 查看100行到300行的内容
cat filename | head -n 300 | tail -n +100
```
## 将程序控制台输出复制到文件
如果仅需要重定向控制台中输出的字符，可以使用`>`或`>>`来实现：
```bash
# 输出到文件output.txt中，如不存在该文件则创建，如存在则覆盖其内容
some_command > output.txt
# 输出到文件output.txt中，如不存在该文件则创建，如存在则追加到文件尾部
some_command >> output.txt
```
如果需要保留控制台的内容，同时输出到文件中，需要用到`tee`命令：
```bash
some_command | tee output.txt
```
有时会使用`tee`命令后控制台有输出，但文件内容为空，此时可能是由于some_command输出的字符从std error文件描述符输出，需要先将std error的输出导向到std output：
```bash
some_command 2>&1 | tee output.txt
```
其中，2代表std error，1代表std ouput，`>&`是linux中fd到fd的重定向操作符。

## 参考文章
1. [shell脚本第一行：#!/bin/bash的含义](https://blog.csdn.net/iot_flower/article/details/69055590)
2. [Linux shell执行source和.的区别](https://blog.csdn.net/rikeyone/article/details/84573385)
3. [ubuntu下source、sh、bash、./执行脚本的区别](https://blog.csdn.net/caesarzou/article/details/7310201)
4. [Linux shell中sh和bash的区别](https://www.cnblogs.com/yyxianren/p/10789968.html)
5. [Linux连续执行多条命令的方法](https://www.jb51.net/article/105993.htm)
6. [Linux使用cat、tail、head查看文件任意几行的数据](https://www.cnblogs.com/OnlyLV520/p/8931765.html)
7. [Shell中将程序控制台输出复制到文件](https://blog.csdn.net/shenck1992/article/details/49661461)
