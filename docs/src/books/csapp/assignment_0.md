# 关于作业

CSAPP的[官方网站](http://csapp.cs.cmu.edu/3e/home.html)为学习这本书的人提供了[几个实验](http://csapp.cs.cmu.edu/3e/labs.html)来亲自动手验证学习的内容。计划在记录读书笔记的同时，将这几个实验完成。

## 环境准备

目前来看只需要Linux系统即可，我是在Win10的Linux子系统中进行实验，目前还没有遇到特别的问题。建议是使用docker构建一个纯净的Linxu系统，ubuntu或centos均可。通过docker的方式见参考文章，这里不再详述。

### 关于Docker

> 容器是一个标准化的软件单元，它将代码及其所有依赖关系打包，以便应用程序从一个计算环境可靠快速地运行到另一个计算环境。<br>
Docker容器镜像是一个轻量的独立的可执行的软件包。包含程序运行的时候所需的一切：代码，运行时间，系统工具，系统库和设置。

> Docker 并非是一个通用的容器工具，它依赖于已存在并运行的 Linux 内核环境。<br>
Docker 实质上是在已经运行的 Linux 下制造了一个隔离的文件环境，因此它执行的效率几乎等同于所部署的 Linux 主机。<br>
因此，Docker 必须部署在 Linux 内核的系统上。如果其他系统想部署 Docker 就必须安装一个虚拟 Linux 环境。

### 运行32位程序

在64位Linux系统中通过gcc/g++编译32位程序很简单，只需要加上`-m32`这个编译选项即可。但如果要运行32位程序，还需要进行一些设置。这一部分的内容最初来自于Github，一个大神在issue里的[回答](https://github.com/Microsoft/WSL/issues/2468)。

#### 1. 安装qemu和binfmt

```shell
sudo apt update
sudo apt install qemu-user-static
sudo update-binfmts --install i386 /usr/bin/qemu-i386-static --magic '\x7fELF\x01\x01\x01\x03\x00\x00\x00\x00\x00\x00\x00\x00\x03\x00\x03\x00\x01\x00\x00\x00' --mask '\xff\xff\xff\xff\xff\xff\xff\xfc\xff\xff\xff\xff\xff\xff\xff\xff\xf8\xff\xff\xff\xff\xff\xff\xff'
```

这一步操作可以通过qemu-i386-static的运行来激活对于i386架构的支持，同时在`/var/lib/binfmts/`生成配置文件，方便以后的重复激活。

#### 2. 安装i386架构和需要的软件

```shell
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install gcc:i386
```

#### 3. 开始与停止

开启服务：
```shell
sudo service binfmt-support start
```
就可以编译运行32位的程序，查看可执行文件的信息进行验证：
```shell
gcc helloworld.c -o helloword
./helloworld
file helloword
```
停止服务：
```shell
sudo service binfmt-support stop
```

## 参考文章
1. [知乎专栏：CSAPP-Lab](https://www.zhihu.com/column/c_1325107476128473088)
2. [Windows Docker安装](https://www.runoob.com/docker/windows-docker-install.html)
3. [如何通俗解是Docker是什么？](https://www.zhihu.com/question/28300645)
4. [Docker容器技术---什么是容器？](https://www.jianshu.com/p/477974212ba8)
5. [让64位的WSL（Windows子Linux系统）支持运行32位程序](https://www.jianshu.com/p/3df082840b40)
