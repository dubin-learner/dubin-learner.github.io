# Install EDA softwares
本文记录一些EDA相关的软件、开源代码安装。

## Synopsys Tools (mainly use PrimeTime2016)
参考文章：[Synopsys EDA Tools安装](https://zhuanlan.zhihu.com/p/564884836)。里面的内容十分详细，这里仅摘录重点内容。

### 安装步骤
#### 1.下载软件
文章中有提供Synopsys Tools 2016安装包百度网盘链接。感谢无私分享，建议自取。

![下载后的所有文件夹](https://pic4.zhimg.com/v2-24cf744714584e227a52277ed236b05b_1440w.jpg)

#### 2.运行`./SynopsysInstaller_v3.2.run`
解压生成setup.csh，需要已安装csh

![运行SynopsysInstaller](https://picx.zhimg.com/v2-3afcb154ce5874ad2b706bdb1cd853bb_1440w.jpg)

#### 3.通过GUI界面安装
给setup.csh增加可执行权限后运行，会打开安装的GUI界面

![安装的GUI界面](https://pica.zhimg.com/v2-0c0149d9c9aed230576acac5dfee3ed2_1440w.jpg)

> 选择好对应的安装包和安装位置即可，（注意：安装包首字母大写，安装位置小写）
>
> 一路Next，该选择的都选上，最后点击finish和dismiss即可
>
> 安装软件的顺序：
>
> Scl11.9 —— Vcs2016 —— Verdi2016 —— DesignComplier2016 —— Primetime2016 —— Formality2015
>
> SpyGlass2016单独安装

界面内容还是比较好理解的。如果出现当前目录不可用、找不到安装文件之类的，可以多探索下子目录。

#### 4.生成Synopsys.dat文件
需要在windows下用注册机（`scl_keygen.exe`）生成，重点是HOST ID Daemon/HOST ID Feature/HOST Name这三项

![注册机使用](https://pica.zhimg.com/v2-254d376d7769e38b7b7681deac5c0be6_1440w.jpg)

#### 5.激活License
这部分内容参考文章中写的似乎比较繁琐，以后有空尽可能整理出一个比较清晰的版本。

> 待整理

目前我已经激活成功，但似乎是每次重启系统后都需要重新激活才行。

### 启动后的问题

#### 库文件缺失（libmng.so.1/libtiff.so.3等）
其实在安装文章中也有提到解决方法，只不过我当时忽略了直接去搜索了。以下是当时的搜索内容：
- [库文件libmng.so.1缺失解决办法](https://blog.csdn.net/immeatea_aun/article/details/81748290)
- [How to solve missing libmng.so.1 in Trusty (14.04) Package is no more available](https://blog.csdn.net/immeatea_aun/article/details/8174829://blog.csdn.net/immeatea_aun/article/details/81748290)
- [How do I install libtiff.so.3?](https://askubuntu.com/questions/44132/how-do-i-install-libtiff-so-3)

核心思路是，软件依赖的库文件版本比较旧，如果本地已安装更新版本的库，做个软链接即可；如果未安装则补充安装后做软链接。

#### 出现Warning`sh：1：syntax error bad fd number`
通常是由于 /bin/sh 链接到了 dash 而非 bash。dash 和 bash 是两种不同的 shell，某些脚本在 dash 下可能无法正常运行。

先运行以下命令检查`/bin/sh`是否指向`dash`：
```bash
ls -l /bin/sh
```
如果输出是`/bin/sh -> dash`，则需要将其更改为指向`bash`。执行下列命令进行链接：
```bash
sudo mv /bin/sh /bin/sh.orig
sudo ln -s /bin/bash /bin/sh
```
完成后再运行一次脚本Warning就消失了。

## Open Source Softwares
这里仅列举几个EDA相关的开源软件，列表如下：
- OpenTimer：开源的静态时序分析工具
- OpenPhySyn：开源的后端物理优化工具
- OpenRoad：开源的前端到后端的全流程工具
- iEDA：开源的全流程工具

其中iEDA是国内团队的作品，[官方介绍网站](https://ieda.oscc.cc/tools/ieda-platform/)，很佩服有这样小众领域的开源作品。
他们的[Bilibili账号](https://space.bilibili.com/1189298533)提供了不少EDA相关知识的视频。

### 一点想法
以我个人的视角来看，相比之下OpenRoad应该还是要更加全面一些。

无论如何，开源精神是值得敬佩的，至少不是“国外一开源，国内就自研”。
在很多国内公司“大跃进”式的发展下，很多上不了台面的手段防不胜防，自研这个词已经在某种程度上被污名化了。
毕竟站着把钱挣了，并不是那么容易的事情。😮‍💨

### 本地安装
安装方法就不过多介绍了，每个工程的READMD都写的挺清楚的。
我尝试在我的MacBook Air M1上安装，最终应该只有OpenTimer成功了，其他的或多或少都有些兼容性问题。

然后就通过OrbStack分别创建了Arm64和AMD64两个版本的Ubuntu20.04虚拟机，不得不说OrbStack确实是好用。
- Arm64：可以成功安装OpenTimer和OpenPhySyn
- AMD64：可以成功安装OpenRoad和iEDA（但是无法启动GUI）

据说Arm64的ubuntu虚拟机效率能达到原生macos的94%左右，但AMD64也就是转译成Intel指令效率只有40%。[参考数据来源](https://www.bilibili.com/video/BV186CPY5EKV)

关于启动GUI，本来搜索到OrbStack和NoMachine联动是可以实现的，甚至有用X11直接转发的教程，但我尝试设置后都失败了，
教程上也有一些语焉不详的地方，后来就干脆直接放弃。可能需要以后买一台intel芯片的电脑主机再用吧。
