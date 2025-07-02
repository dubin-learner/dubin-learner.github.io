# 安装concorde

## 简介
concorde是一个TSP问题求解器（solver），所谓TSP问题就是旅行商问题（Travel Salesman Problem），有一定数目的城市，要求不重复访问完其中每一个城市的最短路径是哪一条。

主要是因为之前有在看《迷茫的旅行商》这本书，讲了旅行商问题的起源、应用等诸多内容，目前大概看到第三章，距离看完仍然遥遥无期。

这本书中提到了concorde是一个性能很不错的求解器，由业内大佬开发，免费给科研人员使用，并且开放了源码。

主站地址：[Travel Salesman Problem](https://www.math.uwaterloo.ca/tsp/index.html)

[下载页面](https://www.math.uwaterloo.ca/tsp/concorde/downloads/downloads.htm) 
对于windows系统，有一个具有图形化界面的安装包，很方便；除此之外还有基本支持全平台的源码安装方案。

![Concorde Windows GUI](https://www.math.uwaterloo.ca/tsp/concorde/gui/img/done.jpg)

PS: 本来公司的笔记本电脑上装了图形化的concorde，然而前一阵子搞保密之类的操作，被判定为非白名单软件给强制卸载了。😮‍💨

## 源码安装

考虑到目前已经是用MacBook Air的时候比较多，虽然不知道后面会不会用，但还是想要试着装一下看。

然而由于apple m1芯片的问题，着实踩了些坑，以下为一些记录。

### 原生系统安装

理论上讲，源码安装只要配置好gcc，成功编译就能顺利完成，然而还是遇到了不明所以的问题。

下载最新的源码包：

Concorde-03.12.19     Dec 19, 2003 ANSI C Code as gzipped tar file

按照官方的方法[安装参考文档](https://www.math.uwaterloo.ca/tsp/concorde/DOC/README.html)，先解压：
```bash
gunzip co031219.tgz
tar xvf co031219.tar
cd concorde/
```
然后配置编译选项进行configure（最好的另一个目录下），最后make安装：
```bash
cd ../
mkdir concorde_build
cd concorde_build
CC="gcc" CFLAGS="-g -O3" ../concorde/configure --host=darwin
make
```
对于macos官方文档中说是要指定host，实测不指定却是会报错，说无法确定host。

然而这种在make过程中会编译报错，大概是`size_t`的类型不支持修改之类的，反正有点莫名其妙，尝试几次无果后放弃。

> 在stackoverflow上搜到了一个相关问题[concorde with apple silicon m1](https://stackoverflow.com/questions/67968517/concorde-with-apple-silicon-m1)，看结果似乎是能正确安装的。

### 通过orbstack的ubuntu安装

之前接触了orbstack，是一种类似docker的方式，可以模拟ubuntu环境。考虑到还是ubuntu更通用一些，这次换成了ubuntu进行尝试，但仍然是apple m1架构，即arm64。

方法上没有什么区别，仍然需要指定host，这里也是指定host为darwin；初期编译顺利，但最后在UTIL模块编译时报错，如下：
```bash
../../concorde/UTIL/safe_io.c:1251:49: error: ‘struct hostent’ has no member named ‘h_addr’
 1251 |     memcpy ((void *) &hsock.sin_addr, (void *) h->h_addr, h->h_length);
      |                                                 ^~
```
还是没有搞清楚原因。

### 通过orbstack的intel架构ubuntu安装

发现orbstack是支持模拟不同的架构安装ubuntu的，果断选择intel amd64版本又安装了一个ubuntu容器。

安装方法和上面没有区别，这次不需要指定host就能用。注意编译安装目录最好不在原始的目录之下，似乎直接在原始目录下安装确实会有问题。

configure比较顺利，但make时会报错：
```
/usr/bin/ld: ../LP/lp.a(lpqsopt.o): in function `CClp_tune_small':
/home/dubin/build/LP/../../concorde/LP/lpqsopt.c:355: undefined reference to `QSset_param'
/usr/bin/ld: /home/dubin/build/LP/../../concorde/LP/lpqsopt.c:361: undefined reference to `QSset_param'
/usr/bin/ld: /home/dubin/build/LP/../../concorde/LP/lpqsopt.c:367: undefined reference to `QSset_param'
/usr/bin/ld: /home/dubin/build/LP/../../concorde/LP/lpqsopt.c:373: undefined reference to `QSset_param'
/usr/bin/ld: ../LP/lp.a(lpqsopt.o): in function `CClp_free':
......
```
总之就是提示link error。查了一下需要指定qsopt编译好的.h和.a文件，具体见[qsopt相关页面](https://www.math.uwaterloo.ca/~bico/qsopt/downloads/downloads.htm)，最终选择的qsopt编译版本为：
```
Ubuntu 18 (with -fPIC)
- qsopt      Solver Executable
- qsopt.a    Function Library (170311)
- qsopt.h    C include file
```

给configure命令添加`--with=qsopt`参数如下：
```bash
CC="gcc" CFLAGS="-g -O3" ../concorde/configure --with-qsopt=/home/dubin/concorde_build/QSOPT/
make
```

就可以成功编译，以上提到的几个编译报错都没有。最终成功生成了./TSP/concorde可执行文件。

通过命令测试运行效果：
```bash
$ ./TSP/concorde -s 99 -k 100
./TSP/concorde -s 99 -k 100
Host: ubuntu-20-intel  Current process id: 5413
Using random seed 99
Random 100 point set
XSet initial upperbound to 780 (from tour)
  LP Value  1: 738.500000  (0.02 seconds)
  LP Value  2: 765.000000  (0.02 seconds)
  LP Value  3: 774.660000  (0.04 seconds)
  LP Value  4: 778.000000  (0.06 seconds)
  LP Value  5: 778.465517  (0.07 seconds)
  LP Value  6: 778.705882  (0.09 seconds)
  LP Value  7: 779.538462  (0.11 seconds)
  LP Value  8: 779.937500  (0.13 seconds)
  LP Value  9: 780.000000  (0.14 seconds)
New lower bound: 780.000000
Final lower bound 780.000000, upper bound 780.000000
Exact lower bound: 780.000000
DIFF: 0.000000
Final LP has 180 rows, 336 columns, 2921 nonzeros
Optimal Solution: 780.00
Number of bbnodes: 1
Total Running Time: 0.22 (seconds)
```
