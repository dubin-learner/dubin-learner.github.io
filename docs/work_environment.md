# 开发环境
本篇主要记录我个人日常工作的开发环境配置。

工作上主要是在linux服务器上进行开发。

vim和tmux都是可以通过快捷键进行操作，可以更加集中的使用键盘（当然鼠标也是会用的）

对于我个人来说是比较习惯的。

## vim配置

原则是尽可能简单可控。
- 简单意味着如果换新的服务器环境，可以快速配置上手；
- 可控意味着基本懂得所有的配置含义，当环境修改时能进行适当的新增或删除。

### 基础配置
这部分配置是vim本身自带的，配置完就能用。

对公司环境和本地电脑环境进行合并；同步更新github的vimrc文件。
这里增加vimrc中的原生可配置内容。

### 一些简单的插件
这部分插件可以提升一些vim的使用体验，当然最大的特点也是即插即用，不需要环境依赖、其他组件依赖。

如果内部服务器无法链接外网，那么复制插件压缩包，解压放到指定目录就能用。
- colors
- pack

目前使用的插件列表：
1. auto-pairs
2. ctrlp（使用频率低）
3. nerdtree
4. vim-airline
5. vim-gitgutter
6. apc

补充对应插件的下载地址，并且在github中进行整理，固定版本保存一份？

补充一些主题，更改vim配色
1. duoduo
2. gruvbox
3. janah
4. monokai

补充vim主题下载网站，固定版本保存。

### 自定义函数
为工作环境增加的一些函数，尽量自己写并增加注释，为了提高一些工作效率。

1. 快速编译：F5，C-F5
2. 更新tags：快速跳转函数
3. 快速格式化：C++ style
4. 快捷键切换：自动补全模式，git gutter
5. 插入注释
6. cpplint检查

这里贴上函数实现的细节，补充部分注释内容。

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

vim tmux shell其实都可以是终端，并且可以嵌套。而且我经常用vim嵌套好几层。
补充用pstree快速查看当前终端的嵌套情况方法：`pstree -s $$`
