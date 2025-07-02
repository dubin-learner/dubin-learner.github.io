# MacOS M1 sonoma安装opencv
其实也没什么原因，图像处理这块的知识我一直都不想荒废；
毕竟本科毕业加上整个研究生期间，都在做相关的内容。

不过工作了这么久，加上中间也换过两次电脑，之前的环境也没有了。
读书的时候是Matlab和C++，基本写原型程序用Matlab，只有很少的时候用C++，OpenCV也接触过一些。
现在C++已经成为我的主力语言，而Matlab基本已经忘光。

这次重新搭建OpenCV的环境，主要是想慢慢捡起图像处理的一些知识，
而且当年也没有学习机器学习相关的内容，我个人对于这种黑盒的东西也有些抵触心理。
现在则是希望能多学点东西，缓解一下自己对于未来和对于自己的焦虑。

言归正传，这次选择python和C++，因为目前使用的比较广泛，
用python可以后续无缝接入tensorflow之类的机器学习；而且OpenCV对这两者都有不错的支持。

Matlab就不再使用了，因为不跨平台MacOS也不方便用；虽然有Octave这种但也算了吧。

想来我还在Cousera上补过Matlab相关的课程呢。
> [Matlab程序设计入门](https://www.coursera.org/learn/matlab) - [我的证书](https://www.coursera.org/account/accomplishments/verify/2WMN3EAYQB6T)

## 安装
安装方法相当简单，直接使用brew安装：
```bash
brew install opencv
pkg-config --cflags --libs opencv4 # 显示安装的opencv相关libs
```
想用源码安装也是可以的，可以看参考文章[1]，这里就不展开了。

## python3部分
有一个比较简单的验证安装是否成功的方法，打开python3的命令行：
```python
import cv2
print(cv2.__version__)
```
如果能够成功import和打印版本号，则证明安装成功。

然后是一个简单的python3程序，可以用来验证：
```python3
import cv2
img = cv2.imread('lena256x256.png')
cv2.imshow('Image', img)
cv2.waitKey(0)
cv2.destroyWindow("Image")
```
可以成功显示每个学习图像处理的同学都会接触到的Lena图。

![Lena图](../resources/lena256x256.jpeg)

## c++部分
简直了，被折腾一天😂。

用于验证的代码如下：
```cpp
#include <iostream>
#include <opencv2/opencv.hpp>
using namespace cv;

int main() {
  Mat image = imread("lena.png");
  std::cout << "after imread" << std::endl;
  if (!image.data) {
    std::cout << "No image data" << std::endl;
    return -1;
  }
  namedWindow("Display Image", WINDOW_AUTOSIZE);
  imshow("Display Image", image);
  waitKey(0);
  return 0;
}
```
编译方法如下：
```bash
g++ test_opencv.cpp -o test `pkg-config --cflags --libs opencv4`
./test
```
一般情况下是能正常编译的，然后运行test可以正常显示Lena图。然而我遇到了编译问题
```bash
fatal error: 'iostream' not found
1 | #include <iostream>
     |          ^~~~~~~~~~
     1 error generated.
```
很奇怪，iostream找不到。我在网上找了半天，终于发现和我升级系统，并且经常更新软件有关。

直接按照参考文章[2]中说的，先把CommandLineTools里的内容全部删除，在重新安装后就能恢复正常。

```bash
sudo rm -rf /Library/Developer/CommandLineTools/
xcode-select --install
```
!> 总结：以后尽量不要用`brew upgrade`升级软件包，保持一个稳定的环境很重要。

## 参考文档
1. [Mac配置OpenCV C++版本](https://www.cnblogs.com/RioTian/p/17409555.html)
2. [c++ compiler not working after macOS sequoia update](https://developer.apple.com/forums/thread/763862)
