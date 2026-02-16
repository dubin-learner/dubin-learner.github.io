# EDA软件安装记录：开源软件
## 写在前面
无论如何，开源精神是值得敬佩的。

很认可iEDA团队的一句话，“开源不是目的而是方式”。商业公司即使无法做到开源，起码的实事求是态度是要有的。然而，国内软件的一个常见现象就是“国外一开源，国内就自研”。更有甚者，很多国内公司搞“大跃进”式发展，通过“放卫星”搞宣传，技术方面就只能用一些上不了台面的手段才能进步。“自研”这个词在某种程度上已经被污名化了，实在是悲哀。

毕竟，站着把钱挣了这件事，并不容易；能有这种决心的公司只能是少数吧。

### 软件列表

多说无益，下面列举我安装过的几个EDA开源软件：
- OpenTimer：开源的静态时序分析工具
- OpenPhySyn：开源的后端物理优化工具
- OpenRoad：开源的前端到后端的全流程工具
- iEDA：开源的全流程工具

其中iEDA是国内团队的作品，[官方介绍](https://ieda.oscc.cc/tools/ieda-platform/)。
他们的[Bilibili账号](https://space.bilibili.com/1189298533)提供了不少EDA相关知识的视频。

同样是全流程工具，以我个人的视角来看，相比之下OpenRoad应该还是比iEDA要更加全面一些。

### 本地安装

安装方法就不过多介绍了，每个工程的READMD都写的挺清楚的。

下面仅记录我尝试在我的MacBook Air M1上安装的结果。

最终应该只有OpenTimer可以在原生系统上安装，其他的或多或少都有些兼容性问题。

通过OrbStack分别创建了Arm64和AMD64两个版本的Ubuntu20.04虚拟机（不得不说OrbStack确实是好用）：
- Arm64：可以成功安装OpenTimer和OpenPhySyn
- AMD64：可以成功安装OpenRoad和iEDA（但是无法启动GUI）

据说Arm64的ubuntu虚拟机效率能达到原生macos的94%左右，但AMD64也就是转译成Intel指令效率只有40%。（[参考数据来源](https://www.bilibili.com/video/BV186CPY5EKV)）

### 已解决 ~~遗留问题~~

可以通过OrbStack和xQuartz用X11转发实现GUI显示，并且已经借助该功能成功启动Synopsys EDA Tools的GUI安装界面。

借助deepseek的回答实现，这部分内容可参见[PrimeTime2016安装](/tool/install_eda2)。

!> NoMachine还是不要碰了。

~~关于启动GUI，本来搜索到OrbStack和NoMachine联动是可以实现的，甚至有用X11直接转发的教程，但我尝试设置后都失败了。~~

~~教程上也有一些语焉不详的地方，后来就干脆直接放弃。可能需要以后买一台intel芯片的电脑主机再用吧。~~

~~这里仅贴上参考过的文章：~~
- ~~[为OrbStack的虚拟机创建图形页面，使用X11转发或NoMachine](https://zhuanlan.zhihu.com/p/30004953074)~~
- ~~[GUI in OrbStack machines - Nick Gregorich](https://www.nickgregorich.com/posts/gui-in-orbstack-machines/)~~
