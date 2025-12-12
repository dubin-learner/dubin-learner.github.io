# Perf安装与火焰图

## 在linux上安装perf工具

以Ubuntu为例，可参考[How to Perform Perf Profiling in WSL2](https://www.scicoding.com/how-to-perform-perf-profiling-in-wsl2/)
```bash
sudo apt install linux-tools-generic
ls /usr/lib/linux-tools/5.4.0-216-generic/perf
```

其中，5.4.0-216-generic是linux的内核版本，和系统版本相关，可能会有差异；但路径基本相同。

在`.bashrc`文件中添加alias方便直接使用：
```bash
alias perf=/usr/lib/linux-tools/5.4.0-216-generic/perf
```

配置完成。

## 尝试用perf分析程序的性能

参见 [用Perf寻找程序中的性能热点](https://zhuanlan.zhihu.com/p/134721612)
以下列举比较直接的使用方法：
```bash
# 判断程序的cpu占用率
perf stat ./program

# 记录采样，默认生成perf.data文件
perf record -F 999 ./program

# 查看采样报告，默认直接读取perf.data
perf report
```

使用`perf report -g`时有可能遇到报错：`Cannot load tips.txt file, please install perf!`。
只需要复制一份tips.txt文件即可。
```bash
sudo mkdir -p /usr/share/doc/perf-tip
wget https://raw.githubusercontent.com/torvalds/linux/master/tools/perf/Documentation/tips.txt
sudo mv tips.txt /usr/share/doc/perf-tip/
```

## 火焰图 FlameGraph

与`perf report`类似，但更加直观的方式是使用火焰图。
需要在Github上[下载Perl脚本](https://github.com/brendangregg/FlameGraph)

以参考文章
[How to Perform Perf Profiling in WSL2](https://www.scicoding.com/how-to-perform-perf-profiling-in-wsl2/)
中的simple.c程序为例：
```c
#include <stdio.h>
#include <unistd.h>
void wait(int ms) {
    usleep(ms * 1000);
}
int main() {
    for (int i = 0; i < 5; i++) {
        printf("Step %d\n", i);
        fflush(stdout);
        wait(100);
    }
    return 0;
}
```
使用如下参数编译程序，然后进行采样，用脚本处理perf.data文件，就能得到svg格式的火焰图。
```bash
# compile simple.c
gcc -O0 -ggdb3 -fno-omit-frame-pointer -o simple simple.c

# sample by perf
perf record -c 1000 -g ./simple
#perf record -e cpu-clock --call-graph dwarf -g -F 99 -p $PID

# generate flame graph
perf script > perf.script
./FlameGraph/stackcollapse-perf.pl perf.script > perf.folded
./FlameGraph/flamegraph.pl perf.folded > perf.svg
```

一般用浏览器就可以打开perf.svg，示例如下：
![flame graph](./perf.svg)

可以直接进行`Ctrl`+`f`来搜索函数名，可以支持一些正则进行模糊匹配。

## 在tcl脚本中控制采样粒度

tcl是EDA领域中最常用的脚本语言。如果仅仅需要分析某个命令的性能，或者流程的一部分性能，应该如何做？

这时候就需要在tcl的特定位置，设置采样开启和关闭。设计思路是通过tcl调用bash执行perf相关命令。
实现方式如下：

```tcl
proc start_perf {target_pid frequency output_file} {
    # Warn if the output file exists
    if {[file exists $output_file]} {
        puts "WARNING: Output file $output_file exists and will be overwritten."
    }
 
    # Construct the command
    set command "perf record -e cpu-clock -g -F $frequency --call-graph dwarf -p $target_pid -o $output_file"
 
    # Start perf and capture the PID
    set perf_pid [exec bash -c $command &]
 
    if {$perf_pid == ""} {
        puts "ERROR: Failed to start perf for process $target_pid."
        return -1
    }
 
    puts "Perf starts for process $target_pid with perf PID $perf_pid."
    return $perf_pid
}
proc stop_perf {perf_pid} {
    # Validate that perf_pid exists and is a valid, positive number
    if {[info exists perf_pid] && $perf_pid > 0} {
        # Try to stop the process and handle any errors
        if {[catch {exec kill -INT $perf_pid} result]} {
            puts "ERROR: Failed to stop perf process $perf_pid. $result."
        } else {
            puts "Perf process $perf_pid stopped."
        }
    } else {
        puts "RROR: Invalid or nonexistent perf PID $perf_pid."
    }
}
```
创建了开启和关闭采样的proc：
- 开启时返回perf采样进程的pid，需要传入被采样进程的pid，采样频率和输出文件名；
- 关闭时通过pid直接kill采样进程。

假设需要分析程序执行某个tcl的性能，例如`update_timing`，使用方法如下：
```tcl
source perf.tcl
set target_pid [pid] # 要采样的进程号
set output_file "perf.data" # 输出文件
set frequency 1000 # 采样频率
 
set perf_pid [start_perf $target_pid $frequency $output_file] # 开始采样，记录对应的perf进程号
# some action
update_timing
stop_perf $perf_pid # 结束采样
```

其中perf.tcl就是开启和关闭采样两个proc所在的文件，在tcl中使用`[pid]`直接获取当前程序的pid。

## 进阶用法？
除了这种监控方式之外，还可以监控程序输出的log。
比如另起一个程序，读取当前程序实时输出的输出log，发现特定的字段就开启/结束采样；
或者多次采样，设置不同轮次的采样输出文件不同的文件名即可。
通常只需要一个bash脚本就能实现，结合实际用途修改即可。
