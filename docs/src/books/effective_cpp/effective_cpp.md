# Effective C++ notes

## 零 · 导读

### explicit关键字

在定义类的构造函数时，是否支持显式的类型转换。

```cpp

```

> 声明为explicit的构造函数要比non-explicit更受欢迎，因为可以禁止编译器执行非预期的类型转换。

### copy构造函数 & copy assignment操作符

> 使用“=”的语法也可以调用copy构造函数。区别的方法：是否有一个新的对象被定义。

> copy构造函数很重要，因为它定义了一个对象如何passed by value（值传递）。

> 函数传递参数常见passed by value，但这并不是一个好主意，因为会调用copy构造函数产生额外的开销。Pass-by-reference-to-const往往是比较好的选择。

### 避免未定义的行为

对于空指针取值（dereferencing）、访问无效的数组索引等。

## 一 · 让自己习惯C++

### 将C++视为一个语言联邦

> 最初，C++只是C加上一些面向对象的特性，最初名称C with Classes。

> 如今，C++已经是一个多重范型变成语言（multiparadigm programming language），同时支持：
> 1. 过程形式（procedural）
> 2. 面向对象形式（object-oriented）
> 3. 函数形式（functional）
> 4. 泛型形式（generic）
> 5. 元编程形式（metaprogramming）

C++的主要次语言：
1. C：区块、语句、预处理器、内置数据类型、数组、指针等等。
2. Object-Oriented C++：类（构造与析构）、封装、继承、多态、动态绑定（virtual函数）
3. Template C++：泛型编程（generic programming）、模板元编程（template metaprogramming，TMP）
4. STL：容器、迭代器、算法、函数对象

> 次语言切换时，需要改变策略才能实现高效编程。如内置（C-like）类型而言，pass-by-value通常比pass-by-reference高效；但对于Object-Oriented C++，由于用户自定义的构造函数和析构函数存在，pass-by-reference-to-const往往更好；对于Template C++尤其如此；但STL的迭代器和函数对象都是在C指针之上产生，所以对于STL的迭代器和函数对象而言，pass-by-value守则再次适用。

### 尽量以const enum inline替换#define

使用宏定义的问题：所使用的名称可能并未进入符号表（symbol table）

使用常量替换#define，需要注意的两种特殊情况：
1. 定义常量指针：string对象通常比`char*-based`更加合适
2. class的专属常量：常量作用域位于class内且至多有一个实体：static const成员。注意初值的设定。

```cpp
```

> `#define`并不重视作用域，一旦被定义，在气候的编译过程中有效（除非被#undef）。因此不仅不能够定义class的专属常量，也不能够提供任何封装性。

> the enum hack：一个属于枚举类型的数值可权充int被使用。

> enum hack更像#define而不像const。
1. 取一个enum的地址不合法，取#define的地址通常也不合法。
2. enum和#define一样绝不会导致非必要的内存分配。（特别是对于比较差的编译器来说）
3. enum hack是template metaprogramming的基础技术。

使用宏实现简单的函数功能：不会招致函数调用的额外开销，但需要变量加括号：
```cpp
// 以a和b的较大值调用f
#define CALL_WITH_MAX(a, b) f((a) > (b) ? (a) : (b))
```

写起来略微繁琐，且仍然可能会有问题：
```cpp
int a = 5, b = 0;
CALL_WITH_MAX(++a, b);    //a被累加两次
CALL_WITH_MAX(++a, b+10); //a被累加一次
```

因此，要使用template inline函数来替代#define写出的宏。
```cpp
template<typename T>
inline void callWithMax(const T& a, const T& b) { //由于不清楚T是什么，所以
  f (a > b ? a : b);                              //采用pass by reference-to-const
}
```
> 可以获得宏带来的效率以及一般函数的所有可预料行为和类型安全性。

> 有了const enum inline，对预处理器（特别是#define）的需求降低了，但并未完全消除。#include仍然是必需品，而#ifdef/#ifndef也继续扮演控制编译的重要角色。

> 总结：
> 1. 对于单纯常量，最好以const对象或者enum替换#define
> 2. 对于形似函数的宏，最好改用inline函数替换#define

### 尽可能使用const

const修饰指针的位置不同，修饰的内容不同，只需要看const相对于`*`的位置：

[指针所指向的数据] `*` [指针本身]

可以这样理解，`*`左边往往是该指针所指向数据的类型，因此修饰所指向的数据；右边基本上就是指针变量的名称，因此修饰指针本身。
