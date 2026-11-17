# Matlab/C/C++/OpenCV2混合编程记录
---

## 2016.7.14 奇异值分解

Matlab中的`svd()`函数（<font color = yellow>singular value decomposition</font>，矩阵奇异值分解），以及相应的OpenCV2调用：

---

## 2016.7.13 异常处理机制

- 异常处理（又称为错误处理）功能提供了处理程序运行时出现的任何意外或异常情况的方法。
- 异常处理一般有两种模型，一种是<font color = red>"终止模型"</font>，一种是<font color = red>"恢复模型"</font>；

### 1. <font color = red>"终止模型"</font>
在这种模型中，将假设错误非常关键，将以致于程序无法返回到异常发生的地方继续执行。一旦异常被抛出，就表明错误已无法挽回，也不能回来继续执行。

### 2. <font color = red>"恢复模型"</font>
异常处理程序的工作是修正错误,然后重新尝试调动出问题的方法，并认为的二次能成功。

对于恢复模型，通常希望异常被处理之后能继续执行程序。在这种情况下，抛出异常更像是对方法的调用--可以在Java里用这种方法进行配置，以得到类似恢复的行为。（也就是说,不是抛出异常，而是调用方法修正错误。）

或者，把try块放在while循环里，这样就可以不断的进入try块，直到得到满意的结果。

### 3. 在C语言中异常处理一般有这么几种方式

1. **使用标准C库提供了abort()和exit()两个函数，它们可以强行终止程序的运行，其声明处于<stdlib.h>头文件中**；
2. 使用assert（断言）宏调用，位于头文件<assert.h>中，当程序出错时，就会引发一个abort()；
3. 使用errno全局变量，由C运行时库函数提供，位于头文件<errno.h>中；
4. 使用goto语句，当出错时跳转；
5. 使用setjmp，longjmp进行异常处理。

仅仅尝试了<font color = red>第一种</font>处理方式，即在可能出现错误的位置进行判断，如果出现错误直接使用exit()函数中止程序，代码片段如下：

```
if ( s.at<float>(2) <= 1e-6*s.at<float>(0) )
{
    cout << "H is ill conditioned" << endl;
    exit(EXIT_FAILURE);
}
```

>参考文章链接：[C语言中的异常处理](http://www.cnblogs.com/vimsk/archive/2010/12/11/1901698.html)

---

- 关于一些C/C++的知识：
C++的`iostream`和C中的`stdio.h`：

C++中的`iostream`头文件是包含`stdio.h`的标准输入输出的，前者范围更广，所含有的内容更多。

---
## 2016.6 - 2016.7

### OpenCV2的矩阵运算：

一、对于已经定义好的OpenCV矩阵变量，如：
```
Mat I, img, I1, I2, dst, A, B;
```

#### 1. 加法
```
I = I1 + I2;                    // 等同add(I1,I2,I);
add(I1, I2, dst, mask, dtype);
scaleAdd(I1, scale, I2, dst);   // dst=scale*I1+I2;
```

#### 2. 减法
```
absdiff(I1, I2, I);             // I = |I1 - I2|;
A - B; A - s; s - A; -A;        // 直接进行减法操作（大小需要一致）
subtract(I1, I2, dst);
```

#### 3. 乘法
```
I = 3 * I;                      // 数乘
I = I.mul(3);                   // 点乘，参数可以是数或同样大小的矩阵;
I = I.mul(I,3);                 // 等价于I = 3*I.^2，可以带多个参数；
C = A * B;                      // 矩阵相乘

Mat::cross(Mat);                // 三维向量(或矩阵)的叉乘，A.cross(B)
Mat::dot(Mat);                  // 2个向量(或矩阵)的点乘，A.dot(B)
pow(src, double p, dst);        // 幂，如果p是整数dst = src^p;其他|src|^p
```

#### 4. 除法（用得比较少）
```
A / B; alpha / A;               // 点除
```

#### 5. 转换
```
I.convertTo(I1, CV_32F);        // 类型转换
cvtColor(src, dst, TYPE);       // 通道（颜色）类型转换
A.t();                          // 转置

flip(I, dst, int flipCode);     // 翻转
// flipCode = 0是上下翻转，>0 时左右翻转, <0 时一起来

resize(src, dst, dst.size());   // 图像src进行形变成dst的大小
```

#### 6. 其他
```
Scalar s = sum(I);              // 各通道求和
Scalar m = mean(I);             // 各通道求平均
 
Mat RowClone = C.row(1).clone();// 复制第2行
```

#### 7. 初始化
```cpp
Mat I = imread("Image.png");    // 直接读取图像进行初始化
 
// 直接生成某种类型的矩阵
Mat I;
I.create(row, col, TYPE);

// 通过矩阵img来初始化矩阵I
Mat I(img, Rect(10, 10, 100, 100));     // 用img的一块初始化I。
Mat I = img(Range:all(), Range(1, 3));  // 所有行，2~3列
Mat I = img.clone();                    // 完全复制
img.copyTo(I);                          // 传递矩阵头（注意顺序）

Mat I(2, 2, CV_8UC3, Scalar(0, 0, 255));
// 等效于产生了一个矩阵I = [  (0,0,255), (0,0,255);
                            (0,0,255), (0,0,255)  ];
 
// 特殊矩阵类型的初始化
Mat E = Mat::eye(4, 4, CV_64F);         // 对角矩阵
Mat O = Mat::ones(2, 2, CV_32F);        // 全一矩阵
Mat Z = Mat::zeros(3, 3, CV_8UC1);      // 全零矩阵

// 如果是简单矩阵的初始化
Mat C = (Mat_<double>(2, 2) << 0, -1, 2, 3); 
 
// 通过关系运算建立一个mask
Mat mask = src < 0;
```

#### 8. 矩阵读取和修改

- 1个通道：

```
for(int i = 0;i < I.rows; ++i)
    for(int j = 0; j < I.cols; ++j)
        I.at<uchar>(i, j) = k;
```
- 3个通道：
```
for(int i = 0; i < I.rows; ++i)
    for(int j = 0; j < I.cols; ++j)
    {
        I.at<Vec3b>(i, j)[0] = b;
        I.at<Vec3b>(i, j)[1] = g;
        I.at<Vec3b>(i, j)[2] = r;
    }
```

- 其他机制：

```
Mat::total();                   // 返回一共的元素数量
int Mat::type();                // 返回他的类型CV_16SC3之类
int Mat::depth();               // 返回深度:CV_16SC3-->CV_16S
int Mat::channels();            // 返回通道数

Size Mat::size();               
// 返回Size(cols,rows)；如果大于2维，则返回(-1,-1)，先宽cols再高rows
 
bool Mat::empty();              
// 如果没有元素返回1,即Mat::total() == 0或者Mat::data == NULL
 
uchar *Mat::ptr(int i = 0)      // 指向第i行
I.rows(0).setTo(Scalar(0));     // 把第一行清零
```

---

二、其他数据结构
```
Point2f P(5, 1);                // 二维点
Point3f P3f(2, 6, 7);           // 三维点
```

>参考文章链接：[OpenCV2的矩阵运算](http://blog.csdn.net/guoming0000/article/details/8629885)

---
## 2016.6.1

### Matlab使用技巧记录：
- 对于char类型的数据，**使用`abs()`函数可以显示Ascii码值**；

---