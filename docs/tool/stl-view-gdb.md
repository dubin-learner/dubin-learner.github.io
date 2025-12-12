# 优化GDB调试打印STL数据结果

从各种回答中，可查到的有两种方式：
- 较早的回答推荐使用stl-view-1.03.gdb文件；
- 较新的回答推荐使用python脚本pretty print。

其实都源自GDB Wiki网站中的[STLSupport页面](https://sourceware.org/gdb/wiki/STLSupport)，简单总结如下：

## GCC Python Scripts: Pretty Printer
要求GDB 7.0以上，直接在gcc的安装目录下查找：
```bash
which gcc
# 以gcc-9.4.0为例，用which gcc命令的结果补全路径
cd /home/.../gcc-9.4.0
find . -name "*libstdcxx*"
```

假设返回的结果为：`./share/gcc-9.4.0/python/libstdcxx`，就可以获得`libstdcxx`所在目录的绝对路径。

如果找不到文件，按照Wiki中建议下载gcc对应版本的文件到本地。

增加下面的脚本到`~/.gdbinit`中：（新增一个后缀为`.gdb`的脚本，在gdb启动后手动source也可以）
```python
python
import sys
sys.path.insert(0, '/home/maude/gdb_printers/python')
from libstdcxx.v6.printers import register_libstdcxx_printers
register_libstdcxx_printers (None)
end
```

据说这样在gdb中直接`print`就能打印优化后的STL数据结果，原本的结果可以用`p /r`显示。

为啥是据说呢？因为在服务器上配置后，直接`print`会报错：
```bash
Python Exception <type 'exceptions.ValueError'> zero length field name in format
```

查了下有可能是因为服务器上Python版本为2.6；看了下pretty printer的脚本应该是支持Python3的。

然而想直接用其他路径的Python3，配置半天没成功，遂放弃。

## GDB script: gdb-stl-views
这个是比较老的方法，我记得刚工作的时候就在用，至于这个脚本至少有十多年的历史。

在STLSupport页面上有下载地址。[`dbinit_stl_views-1.03.txt`](https://www.yolinux.com/TUTORIALS/src/dbinit_stl_views-1.03.txt)

同样是直接加到`~/.gdbinit`中，或者新增脚本等用的时候再source。

然而因为脚本太老，下载路径的时间戳是`2008-09-15`，对于现在gcc的stl实现可能有部分已经不适用。

已知的有：（其他问题随用随处理吧）
- `pstring`打印失败，虽然对于`std::string`的变量可以直接`p var.c_str()`显示`const char *`的结果；
- 不支持`unordered_set`和`unordered_map`。

### 支持`unordered_set`和`unordered_map`

让deepseek读入这个脚本，然后生成`punordered_set`和`punordered_map`的实现。

结果还不错，生成后能运行不报错，但有重复打印元素的问题。查了下相关的底层实现，进行了修正如下：
```
#
# std::unordered_set
#

define punordered_set
    if $argc == 0
        help punordered_set
    else
        set $table = $arg0._M_h
        set $num_buckets = $table._M_bucket_count
        set $num_elements = $table._M_element_count
        
        printf "Unordered set size = %u\n", $num_elements
        printf "Bucket count = %u\n", $num_buckets
        
        if $argc >= 2
            set $total_printed = 0
            set $before_begin = $table._M_before_begin

            set $node = $before_begin._M_nxt
            while $node != 0
                set $value = (void*)($node + 1)
                printf "elem[%u]: ", $total_printed
                p *($arg1*)$value
                set $node = $node._M_nxt
                set $total_printed++
            end
        else
            printf "Use punordered_set <set_var> <element_type> to print elements\n"
        end
        
        printf "\nLoad factor = %.2f\n", (double)$num_elements / $num_buckets
    end
end

document punordered_set
    Prints std::unordered_set<T> information.
    Syntax: punordered_set <set> <T>
    Example:
    punordered_set us - prints size and bucket count
    punordered_set us int - prints all elements, size, and bucket info
end
```
```
#
# std::unordered_map
#

define punordered_map
    if $argc == 0
        help punordered_map
    else
        set $table = $arg0._M_h
        set $num_buckets = $table._M_bucket_count
        set $num_elements = $table._M_element_count
        
        printf "Unordered map size = %u\n", $num_elements
        printf "Bucket count = %u\n", $num_buckets
        
        if $argc >= 3
            set $total_printed = 0
            set $before_begin = $table._M_before_begin

            set $node = $before_begin._M_nxt
            while $node != 0
                set $pair = (std::pair< $arg1, $arg2 > *)($node + 1)
                printf "elem[%u].key: ", $total_printed
                p $pair->first
                printf "elem[%u].value: ", $total_printed
                p $pair->second
                set $node = $node._M_nxt
                set $total_printed++
            end
        else
            printf "Use punordered_map <map_var> <key_type> <value_type> to print elements\n"
        end
        
        printf "\nLoad factor = %.2f\n", (double)$num_elements / $num_buckets
    end
end

document punordered_map
    Prints std::unordered_map<K,V> information.
    Syntax: punordered_map <map> <K> <V>
    Example:
    punordered_map um - prints size and bucket count
    punordered_map um int string - prints all key-value pairs
end
```

使用方法与`pset`和`pmap`相同，需要在指定变量后手动补充key和value的类型。

**注意：类型名中间不能有空格**，例如：
```
punordered_map var_map Pointer*const std::vector<int,int>
```
空格起到分隔参数的作用。

### STL HashTable的结构
这部分用于记录deepseek生成代码的问题原因。

借用参考文章3中的一张图：
![](v2-ea913511315fbefdb96999a7b2d16ca5_1440w.jpg)

原本的逻辑：遍历每个bucket，然后访问每个bucket的链表中的元素。

然而buckets中的链表不是相互独立的，如图中所示，bucket 5的链表最后一个元素，其next指针并不是空；
而是指向bucket 4链表中的第一个元素。

**注意：图里bucket 2并没有数据，有数据的bucket 3 4 5**

并且这个实现顺序并不是固定的，即并不是bucket 1最后一个指向bucket 2第一个，这样依次连接。
按照deepseek的实现必然重复访问，除非能判断当前元素不属于当前bucket，STL代码里是这样做的，但在gdb脚本中很难实现。

正确的做法是使用`before_begin`这个指针，作用是哨兵节点，也是用迭代器遍历的起点。

## 参考文章：
1. [打印STL容器中的内容](https://wizardforcel.gitbooks.io/100-gdb-tips/content/print-STL-container.html)
2. [GCC中unordered set/map的实现原理（Part2图解哈希表结构）](https://zhuanlan.zhihu.com/p/259857549)
3. [C++那些事之彻底搞懂STL HashTable](https://zhuanlan.zhihu.com/p/644205339)
