# 开发环境
本篇主要记录我个人日常工作的开发环境配置。

工作上主要是在linux服务器上进行开发。

Vim和tmux都是可以通过快捷键进行操作，可以更加集中的使用键盘（当然鼠标也是会用的）

对于我个人来说是比较习惯的。

## tmux终端管理

补充一些没啥营养的话，例如如何接触tmux，使用的感受。

### tmux使用学习

记录一些常用的使用方式（大部分是快捷键），或增加一些可能有用现在却没用上功能的分析。

[Tmux使用教程-阮一峰](https://www.ruanyifeng.com/blog/2019/10/tmux.html)

### tmux补充设置
直接照抄参考网页的核心内容。
[保持tmux窗口名更改后不变](https://www.cnblogs.com/zhuzi8849/p/6279297.html)

## 常用的shell命令

理解shell中的进程关系，环境变量继承

[父shell和子shell](https://blog.csdn.net/qq_43808700/article/details/115832946)

Vim tmux shell其实都可以是终端，并且可以嵌套。而且我经常用Vim嵌套好几层。
补充用pstree快速查看当前终端的嵌套情况方法：`pstree -s $$`

---

# 环境配置
内网服务器为CentOS，命令行工具主要是csh。需要通过复制安装包、或者源码编译的方式进行安装。目前常用的工具列表如下：
- Vim8.2
- tmux
- tree
- Python3.6.8（按需安装）

## Vim8.2离线安装
Vim官方的源码托管在github上，直接克隆下来编译即可：
```csh
git clone https://github.com/vim/vim.git
cd vim
./configure
make
```
通常执行`./configure`的时候可以加一些额外的配置选项，例如：`--with-fatures=huge --enable-multibyte --enable-python3interp=yes`等等，只需要按需增加。
由于服务器环境上执行安装需要管理员权限，所以只用编译出来的`./src/vim`执行即可。

此时直接执行`./src/vim`应该会报错`E1187: Failed to source defaults.vim`，这是因为`VIMRUNTIME`环境变量没有设置。

在`~/.cshrc`文件中补充环境变量，增加alias方便启动，并且增加vimdiff：
```csh
# tools path
setenv TOOLS_PATH "~/tools"
setenv VIMRUNTIME "${TOOLS_PATH}/vim-8.2.5172/runtime"
alias vim "${TOOLS_PATH}/vim8.2/src/vim
alias vimdiff "vim -d"
alias v "vim"
```
Vim离线安装就完成了。然后就是进行一些常规配置、增加插件。
最终结果详见[我的Vim配置文件](https://github.com/dubin-learner/myVimConfiguration)，下面是其中部分内容的介绍。

?> 原则是尽可能简单可控。
?> - 简单意味着如果换新的服务器环境，可以快速配置上手；
?> - 可控意味着基本懂得所有的配置含义，当环境修改时能进行适当的新增或删除。

### 基础配置
这部分配置是Vim本身自带的，配置完就能用。

对公司环境和本地电脑环境进行合并；同步更新github的Vimrc文件。
这里增加Vimrc中的原生可配置内容。

### 自定义函数
为工作环境增加的一些函数，尽量自己写并增加注释，为了提高一些工作效率。

1. 快速编译：F5，C-F5
2. 更新tags：快速跳转函数
3. 快速格式化：C++ style
4. 快捷键切换：自动补全模式，git gutter
5. 插入注释
6. cpplint检查

这里贴上函数实现的细节，补充部分注释内容。

### 插件补充
当然还是能访问外网会比较好，不过插件建议尽量不要折腾，**够用就行**。
任何对于第三方工具有依赖的插件，能不用尽可能不要用，配置环境就够费劲了。

通过vim-plug来管理插件，创建如下的目录结构：
```csh
.vim/
├── autoload
├── colors
└── plugged
```
下载plug.vim文件：`https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim`，将这个文件放在autoload路径下。
其他两个目录，colors用来存放第三方的主题，plugged用来存放插件。目前使用的插件列表如下：
- [asyncrun.vim](https://github.com/skywind3000/asyncrun.vim)
- [vim-auto-popmenu](https://github.com/skywind3000/vim-auto-popmenu)    
- [vim-airline](https://github.com/vim-airline/vim-airline)    
- [nerdtree](https://github.com/preservim/nerdtree)  
- [vim-gitgutter](https://github.com/airblade/vim-gitgutter)
- [auto-pairs](https://github.com/jiangmiao/auto-pairs)
- [vim-preview](https://github.com/skywind3000/vim-preview)

### 主题配色
推荐一个第三方主题：[duoduo.vim](https://github.com/kba/duoduo/blob/master/colors/duoduo.vim)
推荐一个[Vim主题网站](https://vimcolorschemes.com/)，可以从上面下载自己喜欢的Vim主题。
我用过duoduo、gruvbox、janah、monokai等。

PS：在第一台服务器上配置时，自动补全的popmenu配色出现了点问题，选项的字体和背景全都是纯黑无法看清。
于是额外修改popmenu选项的配色，cursorline也进行了修改：
```vimscript
highlight PMenuSel ctermbg=lightblue
highlight CursorLine cterm=NONE ctermbg=240
```
该方案参考了[这篇文章](https://www.cnblogs.com/chjbbs/p/6272859.html)

### 将git的diff工具配置为vimdiff
一般情况下，只需要执行命令：`git config --global diff.tool vimdiff`就可以。

但如果是自己编译的Vim，因为服务器上权限的问题，只能通过`alias vimdiff "vim -d"`这种方式覆盖vimdiff命令，但git的config却无法正确使用。

在.gitconfig文件中增加：
```bash
[diff]
    tool = svimdiff
[difftool "svimdiff"]
    cmd = /path/to/your/vim -d $LOCAL $REMOTE
[difftool]
    prompt = false
```
其中，`svimdiff`是自定义的字符串，只要在下面的路径配置正确即可，代表自定义了某个路径下的工具作为diff工具。
参考的这篇文章：[使用.gitconfig配置diff工具](https://dev59.com/yGw15IYBdhLWcg3wxuch)

## tmux离线安装
tmux是一个终端复用器，适合ssh时启动多个终端进行管理。源码同样托管在github上，直接获取源码进行编译：
```csh
git clone https://github.com/tmux/tmux
./configure
make
```

### 安装依赖修复
但tmux有一些依赖库有可能在服务器上没有，例如libevent，就会在执行`./configure`时报错：`configure: error: "libevent not found"`。
需要到[libevent官网](https://libevent.org/)下载后，解压（其实源码也托管在github上）然后编译安装：
```csh
wget https://github.com/libevent/libevent/releases/download/release-2.1.12-stable/libevent-2.1.12-stable.tar.gz
tar xvf libevent-2.1.12-stable.tar.gz
cd libevent-2.1.12-stable
./configure --prefix=/path/your/can/access
make
make install
```
这里在执行`./configure`的时候，需要通过`--prefix=`指定一个当前用户可以正常读写的目录，最后`make install`就不需要管理员权限，可以生成需要的库文件给tmux使用。

安装完成后在`~/.cshrc`中增加环境变量，用于安装和运行tmux：
```csh
setenv LD_LIBRARY_PATH "${LD_LIBRARY_PATH}:/installs/path/your/can/access/lib"
setenv PKG_CONFIG_PATH "${PKG_CONFIG_PATH}:/installs/path/your/can/access/lib/pkgconfig"
```
这一步完成后，在tmux编译过程中也需要指定该目录。最后是否`make install`差别不大，因为`make`这一步已经生成了可执行文件。

?> 如果有其他的库文件缺失，例如ncurses，可参考[这篇文章](https://www.cnblogs.com/mitnick/p/18433990)。

### 设置鼠标行为
通常可以在tmux中设置`set mouse on`来开启鼠标功能。

此时鼠标滚轮可以向上翻，右键会显示一个菜单，但左键选中无法复制，中键无法粘贴。
如果需要复制的话，需要同时按住`Shift`，鼠标左键选中和中键粘贴就可以用了。

这个功能可以在tmux中执行了某个命令，但忘记重定向到文件中时，开启后上翻已经输出的信息。有点像默认的terminal在鼠标滚轮下的行为。
通过`set mouse off`即可关闭。

有可能遇到`set mouse on`之后该功能仍然不生效的情况，这有可能是复制模式没有打开，需要`Ctrl+b`+`[`开启复制模式；退出复制模式也很简单，按`q`即可。

### Vim在tmux内外配色不一致问题
tmux离线安装已经完成。和Vim联合使用时发现一个问题，Vim的配色在终端中正常，但在tmux里使用就会变得异常简陋。
原因见：
- [Why do Vim colors look different inside and outside of tmux?](https://unix.stackexchange.com/questions/348771/why-do-vim-colors-look-different-inside-and-outside-of-tmux)
- [Reset background to transparent with tmux?](https://unix.stackexchange.com/questions/57700/reset-background-to-transparent-with-tmux/321576#321576)（上一条答案中指定的细节）

简单来说就是tmux内部的terminal设置问题，默认的不支持背景颜色擦除（back color erase，bce）。
解决方案就是在启动tmux之前，指定为有bce功能的终端：
```csh
alias tmux "setenv TERM "screen-256color-bce"; ${INSTALLS}/bin/tmux"
```
这样Vim和tmux联合使用算是正常了。

## tree离线安装
tree是一个用树状结构显示目录内容的小工具，C语言实现。官方介绍：[tree](https://www.linuxfromscratch.org/blfs/view/svn/general/tree.html)
可以在github或gitlab下载源码进行编译：
```csh
wget https://gitlab.com/OldManProgrammer/unix-tree/-/archive/2.2.1/unix-tree-2.2.1.tar.bz2
tar xvf unix-tree-2.2.1.tar.bz2
cd unix-tree-2.2.1
make
```
在内网服务器make时出现错误：
```csh
cc1: error: unrecognized command line option "-Wpedantic"
cc1: error: unrecognized command line option "-std=c11"
```
这应该是gcc的版本问题，不支持这两个选项。在Makefile中直接把这两个选项删掉即可。对比如下：
```makefile
#CFLAGS+=-std=c11 -Wpedantic -Wall -Wextra -Wstrict-prototypes -Wshadow -Wconversion
CFLAGS+=-Wall -Wextra -Wstrict-prototypes -Wshadow -Wconversion
```
在`~/.cshrc`增加`alias tree ~/tools/unix-tree-2.2.1/tree`即可。

PS：同样可以修改安装目录通过`make install`安装tree，但工程中没有configure文件，直接改Makefile文件即可。

## Python3.6.8离线安装
这部分就不详细记录了，方法和上面基本一样，下载源码安装包，然后`./configure --prefix=/installs/path; make; make install`即可。

值得注意的就是对于比较老旧的服务器版本，不要安装比较新的python3版本，因为要求安装环境的依赖编译工具版本更新才行。
如果要升级很多基础的依赖版本，那就没有必要折腾；不然容易破环现有的编译环境，得不偿失。
