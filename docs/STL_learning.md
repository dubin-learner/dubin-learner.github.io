# C++ STL API

本文将列举一些C++ STL中的API，基本都是到目前为止在LeetCode上刷题时遇到的，自己却不太熟悉的。

## 随机数生成 `rand`

```
int rand(void)
```
定义所在的头文件<cstdlib>

返回一个范围在0和RAND_MAX之间的伪随机数。

RAND_MAX的值和库相关，但保证至少是32767。我本地的环境中RAND_MAX的值是32767。

因为生成的是伪随机数，所以在没有使用srand()初始化随机数种子的情况下，无论程序第几次运行，每次rand()的返回值都是固定的。

将随机数限定在一定范围之内：

``` cpp
v1 = rand() % 100;        // v1 in the range 0 to 99
v2 = rand() % 100 + 1;    // v2 in the range 1 to 100
v3 = rand() % 30 + 1985;  // v3 in the range 1985-2014
```

为了让每次运行rand()产生的随机数不一样，需要初始化随机数种子，并且每次运行时初始化的种子值不同。比较常见的方案是调用time函数。

time函数返回从1970年1月1日物业开始到现在逝去的秒数，因此每次运行程序时，都会提供不同的种子值。

``` cpp
unsigned seed = time(0);
srand(seed);
cout << rand() << endl;
```
参考文档：
1. [cplusplus.com](http://www.cplusplus.com/reference/cstdlib/rand/)
2. [C语言中文网](http://c.biancheng.net/view/1352.html)

## 
