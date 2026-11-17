---
title: gVim中文乱码问题
---

gVim默认的设置对于中文显示支持并不完全，最常见的就是文件显示乱码和菜单乱码，可以通过更改Vim的配置文件解决。

```
"解决文件显示乱码
set encoding=utf-8
set fileencodings=utf-8,chinese,latin-1
if has("win32")
  set fileencoding=chinese
else
  set fileencoding=utf-8
endif

"解决菜单乱码
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim

"解决控制台输出乱码
language messages zh_CN.utf-8
```

## 参考文章
1. [Gvim中文菜单乱码解决方案](https://blog.csdn.net/laruence/article/details/2603031)
