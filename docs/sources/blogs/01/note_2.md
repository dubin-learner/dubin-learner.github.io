# 阅读笔记：GDB常见使用技巧

本文涉及到的几篇博客：
1. [GDB基础知识一](https://blog.51cto.com/12138867/1910950)
2. [GDB调试之二栈溢出](https://blog.51cto.com/12138867/1914119)

这里是一篇比较全面且工整的gdb基础命令整理：[GDB命令基础，让你的程序bug无处躲藏](https://deepzz.com/post/gdb-debug.html)。本文中所涉及的GDB调试命令，基本上都在工作中使用过。

## 一定要掌握的基础命令

只要在linux下开发C/C++程序，就不可能不接触GDB调试。只要经常使用，一些基础的命令都可以掌握。下面简单罗列一些基础命令：

- `start/s` ：开始调试
- `list/l` : 列出附近行的代码，可加行号作为参数
- `break/b` ：加断点，可加行号在指定行设置断点，无参时默认为当前行；也可以对函数、指定地址设置断点
- `display` ：显示指定的变量，配合断点使用，每次停顿到断点同时，如果存在该变量，会显示它的值
- `info/i` ：显示信息，可加break显示当前已有的断点数目、编号及相应的状态；加display也可显示类似信息
- `disable` ：禁用，可加break与编号来暂时禁用指定编号的断点；同理加display与编号也可禁用指定变量显示
- `enable` ：与disable功能相反，将禁用的断点、变量信息显示重新启用
- `print/p` ：显示变量的值
- `run/r` ：在调试环境下运行目标程序，程序本身需要参数时可以直接加在run后的相应位置
- `delete/d` ：删除，可加break与编号删除指定断点；加display与编号删除指定变量的显示，不可恢复
- `continue/c` ：继续运行
- `next/n` ：单步执行，遇到函数并不会步入
- `step/s` ：单步执行，遇到函数会进入函数内部
- `quit/q` ：退出调试

## 提高调试效率的基础命令

熟练使用以上命令就可以进行简单的调试，但如果要更灵活、调试效率更高，还需要掌握以下的命令：

- 条件断点：`break <line-or-function> if <expr>` 能够更灵活地使用断点
- 源码可视：`gdb file -tui` 进入调试后终端内部分为两个窗口，分别为源码（SRC）和命令（CMD）
- 显示内存：`x /<n/f/u> <addr>` 显示指定地址的内存，x为examine的简写
- 显示栈：`bt`即`backtrace`，显示所有栈帧，可通过`bt full`显示更全面的信息
- 栈跳转：通过`frame <number>`进入不同的栈帧；也可以通过`up`和`down`进入上一层/下一层栈帧
- 显示寄存器：`info reg`
- 反汇编指定函数代码：`disas <function>` 如果无参数默认反汇编当前的函数
- 修改指定变量的值：`print x=5` 

对于其中一些命令详细介绍：

### 源码可视

除了在调试前加上`-tui`参数的方式使源码可视，还可以通过`layout`命令对窗口进行分割：
- `layout src` ：显示源代码窗口
- `layout asm` ：显示汇编窗口
- `layout regs` ：显示源代码或汇编和寄存器窗口
- `layout split` ：显示源代码和汇编窗口 
- `layout next` ：显示下一个layout
- `layout prev` ：显示上一个layout

还可以通过快捷键来修改显示的窗口数目：
- `CTRL + l`：刷新窗口
- `CTRL + x`，再按`1`：单窗口模式，显示一个窗口
- `CTRL + x`，再按`2`：双窗口模式，显示两个窗口
- `CTRL + x`，再按`a`：退出layout，回到传统调试模式

当显示源码窗口时，默认的焦点窗口为源码窗口，使用上下方向键会移动光标的的位置。若想要上下方向键来显示历史命令，可以通过`focus/fs`命令来改变焦点窗口：
```shell
(gdb) info win （查看当前的焦点窗口）
    SRC (36 lines) <has focus>
    CMD (18 lines)
(gdb) fs CMD   （切换焦点窗口为命令窗口）
Focus set to CMD window.
(gdb) info win
    SRC (36 lines)
    CMD (18 lines) <has focus>
```

## 显示内存

examine/x命令可配置参数使用不同的格式显示内存`x /<n/f/u> <addr>`：
- 参数n：正整数，表示显示内存的长度，从当前的地址开始显示几个地址的内容
- 参数f：显示的格式，可选的值：x-十六进制 d-十进制 u-十六进制无符号整型 o-八进制 t-二进制 a-十六进制 c-字符格式 f-浮点数格式
- 参数u：多少字节作为一个值，默认为4字节，可选的值：b-单字节 h-双字节 w-四字节 g-八字节

## 显示寄存器：

```shell
(gdb) info reg
rax            0x5      5
rbx            0x0      0
rcx            0x0      0
rdx            0x0      0
rsi            0x8402260        138420832
rdi            0x1      1
rbp            0x7ffffffee190   0x7ffffffee190
rsp            0x7ffffffee150   0x7ffffffee150    ---> 堆栈指针寄存器，通常会指向栈顶的位置
r8             0x0      0
r9             0x0      0
r10            0x8402010        138420240
r11            0x8402010        138420240
r12            0x8000610        134219280
r13            0x7ffffffee270   140737488282224
r14            0x0      0
r15            0x0      0
rip            0x800079b        0x800079b <main+67> ---> 指令寄存器，包含下一条被执行指令的逻辑地址
eflags         0x206    [ PF IF ]
cs             0x33     51
ss             0x2b     43
ds             0x0      0
es             0x0      0
fs             0x0      0
gs             0x0      0
```
比较常用的寄存器：rsp和rip。可以通过`print/p`来打印某个寄存器的值，例如：`p $rip`。

## 将输出定向到文件

将调试过程中的输出重定向到文件中，如将`info function`的结果输出到文件中：
```shell
(gdb) set logging file <filename>
(gdb) set logging on
(gdb) info function
(gdb) set logging off
```
适合输出内容较多的情况。

## 实例：栈溢出

以下是一个简单的例子，无限递归最终会导致栈溢出的错误：
```cpp
#include <stdio.h>
#include <unistd.h>
#include <string.h>

void call_fault(void) {
  char array[9 * 1024 * 1024];
  memset(array, 0, sizeof(array));
}

void call_test(void) {
  int a;
  a = 1;
  call_fault();
}

int main() {
  call_test();
  return 0;
}
```
如果在Windows下使用Visual Studio来调试的话，会给出一个明显的栈溢出错误。如果在Linux下，往往就不会有明显的提示，而是莫名其妙的crash，使用gdb调试也时也会发现很多数据处于无效值的状态，即很多地址时没有权限访问的（栈帧被破坏）。

进入GDB调试，运行程序后会crash在某一行，提示：
```shell
Program received signal SIGSEGV, Segmentation fault.
0x00000000080007f8 in call_fault () at simple.c:15
```
查看当前的程序内存地址映射信息`info proc mappings`，其中末尾的几行会显示栈的地址范围；同时查看堆栈指针寄存器`rsp`的信息：
```shell
      0x7fffff62b000     0x7fffff62c000     0x1000        0x0
      0x7fffff7d0000     0x7fffff7d2000     0x2000        0x0
      0x7fffff7ef000     0x7ffffffef000   0x800000        0x0 [stack]
      0x7ffffffef000     0x7fffffff0000     0x1000        0x0 [vdso]
(gdb) p $rsp
$1 = (void *) 0x7fffff6ee110
```
明显可以看到堆栈指针已经超出了程序内存中栈地址的映射范围，可以判定为栈溢出的错误。

## 参考文章
1. [gdb调试的layout使用](https://blog.csdn.net/zhangjs0322/article/details/10152279)
2. [gdb查看内存](http://c.biancheng.net/view/7470.html)
3. [x86_64汇编之二：x86_64的基本架构（寄存器、寻址模式、指令集概览）](https://blog.csdn.net/qq_29328443/article/details/107188689)
