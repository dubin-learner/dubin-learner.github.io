# STL源码剖析 - 全排列相关（permutation）

全排列即列举出给定元素的排列组合情况。根据数学上的原理，对于有`n`个不重复的元素的集合，其排列组合的结果有`n!`种情况。因此，全排列的算法在时间复杂度上是`O(n!)`的。

## 基础实现

最常规的实现全排列的方式是递归。假设有`n-1`个元素的全排列，对于其中任意一种排列情况来说，再添加一个新元素，都会增加`n`种排列（即新元素分别放置在第`1`个位置到第`n`个位置，总共`n`种情况）。

以此为基础，可以将`n`个元素的全排列视为`n-1`个元素的全排列扩展而来，而第`n`个元素可以通过交换来放在不同的位置。

代码如下：

```cpp
void permutation(vector<int>& vec, int m) { // vec元素集合，m当前全排列数据的位置，此时需要排列的数据为[m,n)，m从0开始
  if (vec.empty()) return;
  const int n = vec.size();
  if (m == n) { // 排列到了最后的位置，输出一种结果
    for (int v : vec) cout << v << ' ';
    cout << endl;
  } else {
    for (int i = m; i < n; ++i) {
      swap(vec[i], vec[m]);    // 列举出第m个数据为每个元素的情况
      permutation(vec, m + 1); // 固定了第m个元素，对[m+1,n)进行全排列
      swap(vec[i], vec[m]);    // 恢复原来的顺序
    }
  }
}
```

## 去重

上面的这种实现的前提是集合中元素不重复，否则会列出冗余的排列。如何在有重复的集合中进行全排列？重点就是去除重复的排列情况。

对于两个相同的元素来说，如`vec[i]`和`vec[j]`，第`i`个元素进行交换之后产生全排列，和第`j`个元素进行交换的全排列，结果是一样的。因此，同样数值的元素，只需要交换、递归全排列一次即可。

只需要判断第i个元素之前是否存在相同的元素，如果存在则不需要再进行交换和递归。具体的实现可以是用for循环来逐一判断；或者是时间换空间，通过`unordered_set`来判断。


```cpp
void permutation(vector<int>& vec, int m) {
  if (vec.empty()) return;
  const int n = vec.size();
  if (m == n) {
    for (int v : vec) cout << v << ' ';
    cout << endl;
  } else {
    unordered_set<int> s;
    for (int i = m; i < n; ++i) {
      if (s.find(vec[i]) != s.end()) continue;
      swap(vec[i], vec[m]);
      permutation(vec, m + 1);
      swap(vec[i], vec[m]);
      s.insert(vec[i]);
    }
  }
}
```

## 非递归形式

以上是通过递归的方式实现全排列，非递归方式有待补充。

## 下一个排列

如果全排列集合中的元素有优先级，则全排列的所有情况也会有在优先级的差别。例如集合为`{1,2,3}`，则全排列按照优先级（即整数的大小）从小到大的顺序为`123`->`132`->`213`->`231`->`312`->`321`。下一个排列即在该优先级顺序下的下一个全排列。对于`123`来说，就是`132`。

已知一个排列，如何求下一个排列？核心就是交换。从后往前，如果存在一对元素，使得前面的元素优先级低于后面的，那么单纯的交换这两个元素，得到新排列的优先级一定大于原始的排列。这一对元素出现的位置越靠近尾端，两个元素的优先级差距越小，则交换后产生的排列与原始排列的优先级之间的差距越小。因此，首先要找到靠近低位最先出现的这一对元素。

如果这一对元素位于最后，那么交换之后就是下一个排列；否则还要对其他元素进行重新排列。以`132`为例，最靠近尾端且前面元素小于后面元素的一对是`1`和`2`，交换之后得到`231`。只要令交换位置之后的优先级从小到大排列，就会得到下一个排列。即将`31`排列为`13`最后得到`213`为下一个排列。

代码如下：

```cpp
void next_permutation(vector<int>& vec) {
  if (vec.empty()) return;
  const int n = vec.size();
  if (n < 2) return;
  int i = n - 2;
  while (i >= 0 && vec[i] >= vec[i + 1]) --i; // 找到从后向前元素变小的位置
  if (i >= 0) {
    int j = n - 1;
    while (j > i && vec[j] <= vec[i]) --j; // 找到优先级大于且差距最小的位置
    if (j > i) swap(vec[i], vec[j]); // 进行交换
  }
  reverse(vec.begin() + i + 1, vec.end()); // 交换位置之后的元素重新排列
}
```

注意，根据查找从后向前元素变小位置的特性，交换位置`i`之后的元素`[i + 1, n)`一定是降序的。因此直接进行`reverse()`就能实现重新排序，不需要`sort()`。这也是在《STL源码剖析》中看到的。

因为`>=`和`<=`的缘故，出现重复的元素会被跳过，也解决了去重的问题。

## 上一个排列

与下一个排列相反，不再赘述。查找方式类似，只不过要反过来考虑。

```cpp
void prev_permutation(vector<int>& vec) {
  if (vec.empty()) return;
  const int n = vec.size();
  if (n < 2) return;
  int i = n - 2;
  while (i >= 0 && vec[i] <= vec[i + 1]) --i; // 找到从后向前元素变大的位置
  if (i >= 0) {
    int j = n - 1;
    while (j > i && vec[j] >= vec[i]) --j; // 找到优先级小于且差距最小的位置
    if (j > i) swap(vec[i], vec[j]); // 进行交换
  }
  reverse(vec.begin() + i + 1, vec.end()); // 交换位置之后的元素重新排列
}
```

STL中有`next_permutation()`和`prev_permutation()`两个函数，需要添加`algorithm`头文件。

## 参考文章
1. [详解全排列](https://www.cnblogs.com/sooner/p/3264882.html)
2. [全排列算法的理解与实现（递归+字典序）](https://www.jianshu.com/p/50a27d7d2972)
3. [全排列问题——浅谈递归](https://blog.csdn.net/guogangj/article/details/1430090)
