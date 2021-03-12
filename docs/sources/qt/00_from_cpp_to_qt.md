# 从C++到Qt

一篇很早的文章，[原文链接](http://blog.debao.me/zh/2010/11/from-cpp-to-qt/)

毕业后第一份工作的工作内容就是Qt，不得不说Qt提供了太多API，上手门槛很低，同时也会导致学到的东西不多。还是希望能够尽可能多地了解一些原理上的东西，因此这个Qt的系列会记录一些相关的文章。

> 本文舍弃IDE或qmake、cmake等工具的束缚，尝试通过几个例子，一步一步从标准 C++ 的编译过渡到 Qt 的编译。

> 本文涉及的都是最基本的东西，或许可以说，只要你用C++ Qt，不管是通过哪种工具(qmake、cmake、boost.build、qtcreator、vs2008、Eclipse、...)，本文的内容都是需要理解的(尽管真正写程序时，我们都不会直接用C++编译器来编译Qt程序)。

我司的EDA工程项目GUI部分就是通过Qt实现，并且通过qmake来管理整个工程的编译，整个工程由各个子工程组成，分别实现不同的功能。修改子工程后仅需编译这部分，不会影响其他功能（有依赖的情况除外）。

## 例子一：简单的控制台程序

某种程度来说，本文讲解了g++工具的使用。用到的配置选项：

- `-o` 指定生成的可执行文件名称
- `-I` 指定头文件的路径
- `-L` 指定库文件的路径
- `-D` 指定必要的宏
- `-l` 指定需要链接的库

g++在使用时最常接触的选项就是`-o`；其次是`-l`。初次之外还有：

- `-g` 调试选项，编译后的可执行文件带有调试信息，可使用gdb调试
- `-c` 编译和汇编选项，但不进行链接
- `-S` 编译选项，不进行汇编和链接，生成的main.s是程序的汇编结果

言归正传，源程序test.cpp：
```cpp
#include <QtCore/QCoreApplication>
#include <QtCore/QDebug>

int main(int argc, char** argv) {
  QCoreApplication app(argc, argv);
  qDebug() << "hello qt!";
  app.exec();
}
```
从该程序中可以看到，要想能够正常编译和运行，在编译器需要提供QtCore相关的头文件、以及相应的实现库，并在运行时需要链接库文件。

编译命令如下：
```shell
g++ test.cpp -o test -DQT_CORE_LIB -IC:/Qt/Qt5.8.0/5.8/mingw53_32/include -LC:/Qt/Qt5.8.0/5.8/mingw53_32/lib -lQt5Core -std=c++11
```

用到的Qt版本为Qt5.8.0，环境为Windows10，通过安装mingw来调用g++命令。

在编译命令中，`-std=c++11`是在第一次编译失败的信息中提出需要额外添加的。

如果在test的路径下直接运行，大概率会报出找不到Qt5Core运行库的问题。此时，将Qt安装目录下的Qt5Core.dll复制到test路径下即可。
