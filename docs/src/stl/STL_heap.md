# STL源码剖析 - 堆 heap

## 概述

堆不属于STL容器组件，binary max heap是`priority_queue`的底层机制。这里提到的堆都是binary heap，是一种complete binary tree（完全二叉树），即除了最底层的叶子节点外都是填满的；而最低层叶子节点从左到右不能有空隙。

max heap即优先级最高的元素位于堆顶。父节点的优先级总是大于子节点的优先级。

## heap算法

STL中heap的算法总共四个，分别是：
1. 入堆算法`push_heap`
2. 出堆算法`pop_heap`
3. 堆排序算法`sort_heap`
4. 建堆算法`make_heap`

STL中堆的底层实现是`vector`，因为`vector`可以实现O(1)的随机访问，通过交换的方式来调整堆中数据的位置。

如果保留vector中下标为0的元素，从第一个元素开始，以层次遍历的顺序构建完全二叉树，则对于下标为`i`的节点来说，其左右子节点一定是`2*i`和`2*i + 1`。通过类似的下标关系，很容易实现父子节点之间数据的交换、调整。

增加下标0的话，对于下标为`i`的节点，其左右子节点分别是`2*i + 1`和`2*i + 2`；对于下标为`i`的节点，其父节点为`(i - 1) / 2`。

### 入堆算法 `push_heap`

对于已有的堆来说，新建一个新的叶子节点，存放新数据，并将其设置为hole（洞）。此时的堆大概率不满足大顶堆的性质，需要进行调整。通过比较新的叶子节点与其父节点的大小，不断向上调整节点的值，直到满足堆的条件为止。即“上溯”（percolate up）。

STL的核心代码：

```cpp
template <class RandomAccessIterator>
inline void push_heap(RandomAccessIterator first, RandomAccessIterator last) {
  // 注意，此函数被调用时，新元素应已置于底部容器vector的最尾端
  __push_heap_aux(first, last, distance_type(first), value_type(first));
}

template <class RandomAccessIterator, class Distance, class T>
inline void __push_heap_aux(RandomAccessIterator first, 
                            RandomAccessIterator last, Distance*, T*) {
  __push_heap(first, Distance((last - first) - 1), Distance(0), T(*(last - 1)));
  // 新元素位于底层容器最尾端，该位置也是初始的洞位置：(last - first) - 1
}
template <class RandomAccessIterator, class Distance, class T>
void __push_heap(RandomAccessIterator first, Distance holeIndex, 
                 Distance topIndex, T value) {
  Distance parent = (holeIndex - 1) / 2; // 找到父节点
  while (holeIndex > topIndex && *(first + parent) < value) {
    // 当尚未到达顶端，且父节点小于新值（需要调整）
    *(first + holeIndex) = *(first + parent); // 令洞值为父值
    holeIndex = parent;                       // 调整洞的位置为父节点
    parent = (parent - 1) / 2;                // 更新父节点
  } // 持续至顶端，或满足heap的次序特性为止
  *(first + holeIndex) = value; // 令洞值为新值，完成插入操作
}
```

### 出堆算法 `pop_heap`

出堆的顺序就是优先级的顺序，优先级最大的先出，即堆顶先出。此时堆顶产生了一个“洞”。将最后一个子节点填充到这个洞中，此时大概率不满足堆的结构，需要将比较洞的左右子节点，如果其中更大的节点大于洞的值，需要交换调整。通过这种向下的调整，即“下溯”（percolate down），直到满足堆的结构为止。

STL的核心代码：

```cpp
template <class RandomAccessIterator>
inline void pop_heap(RandomAccessIterator first, RandomAccessIterator last) {
  __pop_heap_aux(first, last, value_type(first));
}

template <class RandomAccessIterator, class T>
inline void __pop_heap_aux(RandomAccessIterator first,
                           RandomAccessIterator last, T*) {
  __pop_heap(first, last - 1, last - 1, T(*(last - 1)), distance_type(first));
  // 出堆的操作：将底部容器中第一个元素和最后一个元素交换，堆长度减一
  // 调整当前堆长度下的结构使其满足堆结构，即范围为[first, last - 1)
}

template <class RandomAccessIterator, class T, class Distance>
inline void __pop_heap(RandomAccessIterator first, RandomAccessIterator last,
                       RandomAccessIterator result, T value, Distance*) {
  *result = *first; // 令尾值为首值，此时value中仍保留了原来的尾值
  __adjust_heap(first, Distance(0), Distance(last - first), value);
}

template <class RandomAccessIterator, class Distance, class T>
void __adjust_heap(RandomAccessIterator first, Distance holeIndex,
                   Distance len, T value) {
  Distance topIndex = holeIndex;
  Distance secondChild = 2 * holeIndex + 2;  // 洞节点的右子节点
  while (secondChild < len) {
    // 比较洞节点的左右两个子值，然后以secondChild代表较大的节点
    if (*(first + secondChild) < *(first + secondChild - 1))
      secondChild--;
    // 下溯（percolate down）：令较大子值为洞值，再令洞号下移至较大节点处
    *(first + holeIndex) = *(first + secondChild);
    holeIndex = secondChild;
    // 找出新洞节点的右子节点
    secondChild = 2 * (secondChild + 1);
  }
  if (secondChild == len) { // 没有右子节点，只有左子节点
    *(first + holeIndex) = *(first + secondChild - 1);
    holeIndex = secondChild - 1;
  }
  *(first + holeIndex) = value;
}
```

注意，在`pop_heap`之后，最大元素只是被放置于底部容器的最尾端，并没有移除。可以通过`vector`的`back()`来进行取值，需要移出的话需要使用`pop_back()`。

### 堆排序算法 `sort_heap`

根据堆的性质，每次出堆都是所有数据中优先级最高的。将所有数据依次出堆，按照`pop_heap`的策略每次将出堆的数据放到有效堆数据的尾端，当所有数据都出堆之后，就得到了一个优先级递增的序列。

注意，经过`sort_heap`之后的数据结构已经不是一个合法的堆了。

STL中的核心代码：

```cpp
template <class RandomAccessIterator>
void sort_heap(RandomAccessIterator first, RandomAccessIterator last) {
  while (last - first > 1) {
    pop_heap(first, last--); // 每执行pop_heap()一次，操作范围即缩小一个
  }
}
```

### 建堆算法 `make_heap`

STL中建堆的思路是自底向上的，从数据最底层的父节点开始，调整该节点和左右子节点的结构，使其符合堆的结构（父节点的优先级大于子节点），逐步向上调整。

```cpp
template <class RandomAccessIterator>
inline void make_heap(RandomAccessIterator first, RandomAccessIterator last) {
  __make_heap(first, last, value_type(first), distance_type(first));
}

template <class RandomAccessIterator, class T, class Distance>
void __make_heap(RandomAccessIterator first, RandomAccessIterator last,
                 T*, Distance*) {
  if (last - first < 2) return;       // 数据为空或只有一个元素时无需调整
  Distance len = last - first;        // 数据边界
  Distance parent = (len - 2) / 2;    // 最后一个父节点
  while (true) {
    __adjust_heap(first, parent, len, T(*(first + parent)));
    if (parent == 0) return;          // 最顶层节点调整后，建堆完成
    parent--;
  }
}
```

感觉还是存在令一种思路的，先设定当前堆中仅有第一个数据，将后面的数据逐个入堆，直到最后一个元素。

```cpp
template <class RandomAccessIterator, class T, class Distance>
void __make_heap_via_push(RandomAccessIterator first, RandomAccessIterator last, 
                          T*, Distance*) {
  if (last - first < 2) return;
  Distance holeIndex = 1, len = last - first;
  while (holeIndex < len) {
    __push_heap(first, holdeIndex, Distance(0), *(first + holdeIndex));
    holeIndex++;
  }
}
```

## 参考文档

1. [STL之heap相关操作算法](https://blog.csdn.net/jxh_123/article/details/34853099)
