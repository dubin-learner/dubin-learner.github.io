# C++ Visual Studio debug模式下的内存错误提示

在VS的debug模式下进行C++开发，当使用new/delete进行内存操作时，VS会在不同的情况下对内存进行赋值，方便调试时使用。最常见的就是0xcdcdcdcd和0xdddddddd这两种了。

## 0xcdcdcdcd：在堆上分配但未使用的内存

**C**D表示**C**lean Memory，即没有使用的“干净”的内存。在调试中遇到印象比较深的一次是画眼图的程序，画布上显示颜色的方格分配了内存但没有赋初值，在debug模式下还没画眼图画布上就显示了颜色。release模式下则不存在这种情况，因为release模式下分配的内存初值都是0。

## 0xdddddddd：在堆上分配过已经释放的内存

**D**D表示**D**ead Memory，表示已经释放的“死掉”的内存。这个就比较常见了，尤其是在操作指针时，释放了指针所指向的内存但指针没有置为空。一般发现0xdddddddd都是已经造成了内存的非法访问了。😀

## 其他情况：

除了常见的这两个，还有其他的提示，如下图：

![1568274857582](C:\Users\dubin1.FMSHZJ\AppData\Roaming\Typora\typora-user-images\1568274857582.png)

图片来自博客[Win32 Debug CRT Heap Internals](http://www.nobugs.org/developer/win32/debug_crt_heap.html#table)，其中提到的内容比较全面了。先留个空，准备花点时间读一下。参考博客【1】中还提到了一篇文章，提到了VS调试中的一些技巧。

参考文章：

> [【1】 0xcdcdcdcd是什么？（博客园）](https://www.cnblogs.com/fresky/archive/2012/07/06/2579467.html)
>
> [【2】令人蛋疼的错误提示 0xcdcdcdcd 0xdddddddd ...（博客园）](https://www.cnblogs.com/pcchinadreamfly/archive/2012/04/26/2471317.html) 

