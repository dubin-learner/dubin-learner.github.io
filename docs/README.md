# 关于我

> last update time: 2024/03/27

准备整理好好整理一下，利用工作之余建立自己的知识体系。

只能说万事靠自己！多积累一些总是没有错的。

万恶的加班，希望以后能少加班。把自己的时间还给自己。

---

对工作有不切实际的期望，是因为太过年轻幼稚。应该认清现状，工作是工作，是实现人生价值的一部分，但最多也只是一部分。自我满足、成就感还应该从自己的兴趣出发。

而且很重要的一点是，在工作中学习是一种奢望，学习新的东西从来都不是被动的。成长都是要靠自己。

降低对他人的期望，是对别人好，对自己更好的事情。

---

有些话，不吐不快。公司最近又开始强调考勤的事情了。本来，公司对外宣称是弹性是一定的弹性工作时间，早上上班有半个小时的缓冲，听起来像是一个员工福利。然而却几次三番强调，公司不希望员工去用这半个小时的缓冲，似乎用这半个小时还要影响绩效考核之类的。

实话说，贱不贱啊？要不然就别给这半个小时，适应了也就这样了；要不然给了就别唧唧歪歪。不明白这是什么水平的管理者，才会在这些事情上搞的不清不楚。

---

在硬件公司工作的软件工程师，擅长日常摸鱼。

---

2023.6.12更新：关于本专业相关的内容，参考[EDA Wiki](https://openbelt.org.cn/wiki/intro/course/)。值得注意的是，除了VLSI logic/layout这门课之外，其他的都不太容易找到project进行练习。这里考虑了一下，可以通过看[OpenPhySyn](https://github.com/scale-lab/OpenPhySyn)的内部实现（虽然感觉还是读公司的code更合适一些，但不开源就不能放在博客里），讨论其中Physical Optimization的一些原理，以及其内部引用的OpenSTA也可以学习一下。

---

2023.6.9更新：间隔时间有点久。这两年还在原来的领域，但感觉学习到的新东西没有达到我的预期。因此需要重新规划一下。
其实我不是一个擅长听课的人，以前在学校的时候，上课学习的时候不太多，大多数都是期末考前突击。因此搜索大量的课程计划学习似乎不太现实。
不过还是要有所计划，先选择1~2门比较经典的课程开始好了。初步设想是CS50 Harvard和Nand2teris。

---

2021.8.7更新：重点还是应该放在专业技能上。最近需要补充的基础知识：VLSI CAD layout、Git、Makefile、Regular Expression。

补充：这是因为上次更新的时候是想要换工作，但没有明确目标；这次更新已经换完工作，从事的还是原来的方向，因此想继续强化专业技能。

---

2021.6.12更新：今天在公众号上看到了一篇[推文](https://zhuanlan.zhihu.com/p/377154343)，其内容是个人的社招经历，因为查看了一下履历感觉的确是大神级别的人物，所以经历上可能没啥参考价值，但其中提到了一些他学习的课程，基本涵盖了以上提到的比较欠缺的几个部分，内容为：MIT 6.NULL，MHRD游戏，Stanford CS144和MIT 6.S081。在他自己的知乎账号中还有相关的文章，后续可以作为自己提升的一个参考。

---

2021.6.15正在修改的页面：
- [单调栈和单调队列](src/al/00.md)
- [字符串匹配算法](src/al/01.md)
- [各种排序算法](src/al/03.md)
- [红黑树](src/al/04.md)
- ......

最近要完成的：
1. 读书笔记，先是effective C++，然后是CSAPP
2. 希望每次在Leetcode上遇到的hard都记录一篇
3. 最近在读的espresso逻辑优化源码

未来要完成的：
1. 从零开始完成一个文本编辑器，参考[Neatpad](http://www.catch22.net/tuts/neatpad/neatpad-overview#)；[仅有一篇的翻译](https://blog.csdn.net/keminlau/article/details/4101971)
2. 或者再开始Neatpad之前[用Qt先完成一个文本编辑器](https://blog.51cto.com/1691647/1710939)，算是简单复习一下Qt
3. 国内[南京大学计算机基础实验](https://nju-projectn.github.io/ics-pa-gitbook/ics2019/)，应该是类似CSAPP的课程
3. 操作系统的相关公开课**MIT 6.S081** [知乎专栏](https://www.zhihu.com/column/c_1294282919087964160)、[Github](https://github.com/huihongxiao/MIT6.S081/tree/master/lec01-introduction-and-examples)，之后也可以进行**MIT 6.828**[知乎文章](https://zhuanlan.zhihu.com/p/74028717)

比较欠缺的知识：
1. 计算机网络：这个本科的时候没有学过，后来读研、工作基本没有用到，导致一窍不通。《计算机网络》这本书有纸质版，如果要学习的话还需要找一门公开课的教程。最好配合工具（Wireshark）边实验边学习，可以参考[这篇文章](https://mp.weixin.qq.com/s/WDW1lceGhFBhY6bfAmZfoQ)作为学习计划的指导。结合书中的[实验](https://blog.csdn.net/Beeeeeea/article/details/83786715)。
2. 数据库：同样，没学过也没用过。后续可以考虑制定一下学习计划，待定。[这篇文章](https://mp.weixin.qq.com/s/6qhK1oHXP_VzfgR9BjYVJg)最后提到了Redis源码的学习方法，推荐书籍[《Redis设计与实现》](https://book.douban.com/subject/25900156/)《Redis实战》。
3. 设计模式：优化代码设计，需要一定的经验积累。[参考文章](https://mp.weixin.qq.com/s/DgnYYWSKMItSbe_e34ukQQ)里面提到的[参考网站](https://refactoring.guru/)有不同设计模式的各种语言实现，值得一看。
4. 操作系统：推荐书籍《30天自制操作系统》[Github相关代码](https://github.com/yourtion/30dayMakeOS)，推荐入坑文章[我的操作系统梦破灭了](https://mp.weixin.qq.com/s/KT6ADNGRLrDA8yQ-pvNBVg)
5. 编译原理：
[Let's Build A Simple Interpreter 系列](https://ruslanspivak.com/lsbasi-part1/#)、
[手把手教你构建C语言编译器 系列](https://lotabout.me/2015/write-a-C-interpreter-0/)、
[编译原理实验：Flex(scanner)与Bison(parser)实现计算器](https://my.oschina.net/liuyuanyuangogo/blog/3090065)、
[A small C11 compiler in C++11](https://hub.fastgit.org/wgtdkp/wgtcc)
