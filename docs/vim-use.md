# Vim常见使用技巧

本文将记录一些常见的Vim使用技巧，基本上都是在工作中使用到的。（[Vim Cheat Sheet](https://vim.rtorr.com/lang/zh_cn/)）

## 查找
### 查找高亮
查找字符串比较简单，在命令行模式下输入斜杠`/`，后面接需要查找的模式即可。为了不匹配到其他字符串中的字串，例如查找`bc`但不希望匹配到`abcd`，可以通过转义后的尖括号加以限制`/\<bc\>`

快捷键：通过`Shift` + `*`对光标当前位置的字符串快速选中并查找下一个位置。
### 取消查找高亮
通过命令实现取消，完整命令为`:nohlsearch`，或者使用缩写`:noh`。

## 删除、替换
### 删除行尾的^M
Windows/Dos下的换行符为`\r\n`，而Linux/Unix下的换行符为`\n`，导致Windows下产生、编辑过的文本，在Linux下打开时换行的位置会多一个`\r`字符，被显示^M。通过命令删除（替换为空）：
```shell
:%s/\r//g
```

### 显示匹配模式的数目
命令很简单，可以加入正则表达式进行灵活匹配：
```shell
:%s/pattern//gn
```

### 删除包含特定模式的行
```shell
:g/pattern/d
```
例如删除空行：`:g/^$/d`

### 删除不包含特定模式的行
```shell
:v/pattern/d
```

### 对每行只保留特定模式而删除其他内容
```shell
:%s/^.*\(pattern\).*$/\1/g
```
本质上是Vim中字符串的替换，这里用到了正则表达式中的反向引用"\1"，即引用匹配中第一个组（第一个小括号内）的内容。注意在Vim的命令行中小括号并不是特殊字符，需要加转义字符'\'才有分组功能。

### 删除包含特定字符串的行，并在删除前提示
```shell
:%s/^.*pattern.*$//c
```
本质上还是替换，用空字符替换一整行。

### 删除命令实例
- 处理字符串`/123/456/789/109/example.txt`，怎么删除到最后一个`/`，然后得到`example.txt`？

**答：** `0dte`。其中，`0`：移动到行首，`dte`：删除到第一个字母`e`的位置。

- 处理字符串`/123/456/789/ef/109/example.txt`，怎么删除到最后一个`/`，然后得到`example.txt`？

**答：** `$T/d0`。其中，`$`：移动至行尾，`T/`：从后向前搜索到第一个`/`字符的位置，`d0`：删除到行首。或者`d/ex`，删除到第一个`ex`出现的位置。

## 添加信息
### 添加和删除多行注释
可以通过Vim的可视模式进行实现。在命令模式下，按键`v`、`Ctrl` + `v`和`Shift` + `v`会进入不同的可视模式：
- `v`：常规的可视模式，单个字符选择模式
- `Ctrl` + `v`：块选择模式，可选择块状区域进行操作
- `Shift` + `v`：行选择模式，以行为单位进行选择

对于C/C++的多行注释，即`//`来说，就可以通过块选择模式来进行添加或删除。

### 添加作者相关信息
添加对按键`F4`的映射，并预置一段代码（简单举例）：
```shell
map <F4> ms:call AddSimpleTitle()<CR>
function AddSimpleTitle()
  let n = line('.')
  call append(n + 0, "# *****")
  call append(n + 1, "")
  call append(n + 2, "# * Create time  : ".strftime("%Y-%m-%d %H:%M"))
  call append(n + 3, "# * File name    : ".expand("%:t"))
  call append(n + 4, "")
  call append(n + 5, "# *****")
endfunction 
```

## 光标移动相关
> [Vim光标快速移动技巧总结](https://blog.csdn.net/llzhang_fly/article/details/80474966)
> waiting for writing ...

## 复制与粘贴（使用系统剪切板）
> [Vim在系统剪切板的复制与粘贴](https://blog.csdn.net/zhangxiao93/article/details/53677764)
> waiting for writing ...

## 其他
### 跳转命令
在源文件中如果指定了头文件，比如`#include "utility/utility.h"`这种形式，可以通过快捷键组合`g` + `f`实现快速跳转到utility/utility.h文件中。

### 插件ctags的使用
在已经安装ctags的前提下，在源文件目录下，直接执行（对于C++）生成tags文件：
```shell
ctags -R --c++-kinds=+px --field=+iaS --extra=+q
```
其中，`c++-kinds`用于指定C++语言的tags记录类型，通用格式：`--{language}-kinds`；`field`用于指定每条标记的扩展字段域；`extra`用于增加额外的条目，参数`q`为每个类增加一个条目，参数`f`为每个文件增加一个条目。

在Vim中指定目标路径下使用tags文件：
```shell
:set tags=./tags
```
在代码更改后只需执行`ctags -R`即可将tags进行同步更新。在Vim中使用tags的信息：
- 查找函数或变量的定义位置快捷键`Ctrl` + `]`，或使用命令`:ta name`
- 从函数或变量定义的位置跳转回查找的位置`Ctrl` + `t`
- 向前跳转/向后跳转：`Ctrl` + `i` / `Ctrl` + `o` <font color = blue>这个命令和ctags无关</font>

初步配置完成之后，通常`Ctrl` + `]`会默认跳转到找到的第一处定义的文件中，如果需要先列出所有同名定义的位置，需要组合键`g` + `Ctrl` + `]`。可以通过按键映射的方式修改：
```shell
map <c-]> g<c-]>
```
### Git Gutter插件相关
配置Git Gutter插件之后，可以直接高亮本地的改动：
```shell
set g:gitgutter_enable=1
let g:gitgutter_highlight_lines=1
let g:gitgutter_sign_added='A'
...
nnoremap <silent> <leader>d :GitGutterToggle<cr>
```
通过直接在命令模式下输入`:GitGutterToggle`，可以直接控制Git Gutter插件启用或关闭。`highlight_lines`会背景高亮有改动的代码，`sign_added`表示新添加的代码前会有`A`表示，此外可以修改`sign_modified`、`sign_removed`等不同类型改动代码前的表示。

### 设置快捷键进行编译
通过按键映射，可以指定某个按键来启动编译。如下：
```shell
noremap <F5> : call CompileProject()<CR>
function! CompileProject()
  if filereadable('configure')
    execute "!./configure 30"
  endif
endfunction
```
其中，execute运行可执行文件，`filereadable()`用于判断文件是否存在。

### 自带的文件浏览器netrw
如果可以装插件的话，可以使用nerdtree；没有联网条件使用vim自带的netrw也勉强可以。配置也很简单：
```shell
"设置目录列表的样式：树型
let g:netrw_liststyle=3
"水平分割时，文件浏览器始终显示在左边
let g:netrw_altv=1
"设置文件浏览器窗口宽度为25%
let g:netrw_winsize=20
```
最后一项设置，以当前文档打开的窗口为基准。如果已经水平分割，那么是在50%的基础上进行25%。

## 参考文章
1. [Vim的匹配删除](https://blog.csdn.net/yrx0619/article/details/81032610)
2. [Vim替换反向引用，模式匹配回溯引用...](https://www.qinziheng.com/vim/5651.htm)
3. [Vim删除行尾的^M](https://www.cnblogs.com/wangkongming/p/4624524.html)
4. [Vim的高亮搜索](http://www.voidcn.com/article/p-hrozitlh-zm.html)
5. [Vim中自动添加注释 添加文本信息](https://blog.csdn.net/yusiguyuan/article/details/41090709)
6. [Vim插件ctags的安装与使用](https://www.cnblogs.com/zl-graduate/p/5777711.html)
7. [ctags跳转错误](https://segmentfault.com/q/1010000003734392)
8. [Vimscript判断文件是否存在](https://wxnacy.com/2019/02/21/vimscript-file-exists/)
9. [玩转Vim自带的文件浏览器netrw](https://cloud.tencent.com/developer/article/1891433)
