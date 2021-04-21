# 每日博客笔记

博客地址：[C++全局变量初始化的一点总结](https://www.cnblogs.com/catch/p/4314256.html)。来自于微信公众号“程序喵大人”的每日推文，对该文章进行了转载。

该文章主要内容涉及C++全局变量初始化，属于必须掌握的知识。

## 原文知识点

概括来说，全局变量初始化分为：
- 静态初始化
  - zero initialization
  - const initialization
- 动态初始化

静态初始化**优先于**动态初始化。

静态初始化在编译期即可确定变量的值，动态初始化需要在运行期才能确定，例如将某个函数的返回值赋值给全局变量。

zero initialization也是默认的初始化方式，这类全局变量位于BSS段，只描述大小，不增加目标文件的体积；const initialization这类全局变量位于Data段，会直接增加目标文件的体积。

出现在同一个编译单元中，初始化的顺序与声明顺序一致，销毁顺序相反。（与多个相同作用域的局部变量初始化、销毁顺序类似）不同编译单元的全局变量，其初始化与销毁的顺序取决与编译器的具体实现。

<font color = red>核心问题</font>：如果出现不同编译单元间全局变量的相互引用如何销毁？

### Niffy Counter

个人感觉有点像智能指针`shared_pointer`的实现，通过计数来判断当前变量是否被其他变量引用，归零之后销毁变量。代码如下：

```cpp
// global.h
#ifndef _global_h_
#define _global_h_
extern X x;
class initializer {
  public:
    initializer() {
      if (s_counter_++ == 0) init();
    }
    ~initializer() {
      if (--s_counter_ == 0) clean();
    }
  private:
    void init();
    void clean();
    static int s_counter_;
};
static initializer s_init_val;
#endif
```
头文件的代码比较直白，如果`s_counter`从零开始增加，则初始化变量；`s_counter`归零，则销毁变量。
```cpp
// global.cpp
#include "global.h"
// need to ensure memory alignment??
static char g_dummy[sizeof(X)];
static X& x = reinterpret_cast<X&>(g_dummy);
int initializer::s_counter_ = 0;
void initializer::init() {
  new(&x) X;
}
void initializer::clean() {
  (&x)->~X();
}
```
源文件里直接使用`char`类型申请若干个字节的的内存，然后通过`reinterpret_cast`将该内存重新解读为类`X`。因为`reinterpret_cast`不对内存做修改直接重新解读，在内存没有对齐的情况下的确可能出现问题。

在初始化变量时，直接通过placement new操作进行。

### Placement New

> 本质上是对`operator new`的重载，定义于`#include <new>`中。它不分配内存，调用合适的构造函数在指针所指的地方构造一个对象，之后返回实参指针。

感觉就是placement的英文原义，即将指针“放置”到一块已经分配好的内存上，并构造对象。

如果不是重载过的`operator new`，完成的功能有两项：分配内存，构造对象。`operator delete`与之相反：析构对象，回收内存。

## 参考文章
1. [C++中使用placement new](https://blog.csdn.net/linuxheik/article/details/80449059)
