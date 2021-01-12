# STL源码剖析 - 优先队列 priority_queue

## 概述

相比于普通的队列`queue`，优先队列是在此基础上加入了权值。`priority_queue`内部的元素并非按照被推入的次序排序，而是按照权值的排列（**通常权值以实值表示**）。权值最高者，排到最前面。

缺省情况下`priority_queue`利用max-heap实现。max-heap即大顶堆，是一个以vector为基础的完全二叉树。

## 定义完整列表

由于`priority_queue`完全以底部容器为基础，再加上heap处理规则，因此实现非常简单。缺省情况下以`vector`为底部容器，源代码很简短。

`queue`、`stack`这种以底部容器为基础，通过修改接口来完成其所有工作，被称之为adapter（配接器或适配器）。因此，STL priority_queue往往被归类为adapter而不是container（容器）。

源代码：

```cpp
template <class T, class Sequence = vector<T>,
         class Compare = less<typename Sequence::value_type> >
class priority_queue {
  public:
    typedef typename Sequence::value_type value_type;
    typedef typename Sequence::size_type size_type;
    typedef typename Sequence::reference reference;
    typedef typename Sequence::const_reference const_reference;
  protected:
    Sequence c;      // 底层容器
    Compare comp;    // 元素大小比较标准
  public:
    priority_queue() : c() {}
    explicit priority_queue(const Comapre& x) : c(), comp(x) {}

  // 以下用到的make_heap()，push_heap()，pop_heap()都是泛型算法
  // 注意，任何一个构造函数都立刻于底层容器内产生一个implicit representation heap
    template <class InputIterator> priority_queue(InputIterator first, InputIterator last, const Compare& x) : c(first, last), comp(x) { make_heap(c.begin(), c.end(), comp); }
    template <class InputIterator> priority_queue(InputIterator first, InputIterator last) : c(first, last) { make_heap(c.begin(), c.end(), comp); }

    bool empty() const { return c.empty(); }
    size_type size() const { return c.size(); }
    const_reference top() const { return c.front(); }
    
    void push(const value_type& x) {
      __STL_TRY { // __STL_TRY/__STL_UNWIND是异常处理
        // push_heap是泛型算法，先利用底层容器的push_back()将新元素推入末端，再重排heap
        c.push_back(x);
        push_heap(c.begin(), c.end(), comp);
      }
      __STL_UNWIND(c.clear());
    }
    void pop() {
      __STL_TRY {
        // pop_heap是泛型算法，从heap内取出一个元素。它并不是真正将元素弹出，而是重排heap，然后再以底层容器的pop_back()取得被弹出的元素。
        pop_heap(c.begin(), c.end(), comp);
        c.pop_back();
      }
      __STL_UNWIND(c.clear());
    }
};
```

## 没有迭代器

`priority_queue`的所有元素，进出都有一定的规则，只有queue顶端的元素（权值最高者），才有机会被外界取用。`priority_queue`不提供遍历功能，也不提供迭代器。

## 测试实例

```cpp
#include <queue>
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
  // test priority queue ...
  int ia[9] = {0,1,2,3,4,8,9,3,5};
  priority_queue<int> ipq(ia, ia+9);
  cout << "size = " << ipq.size() << endl; // size = 9

  for (int i = 0; i < ipg.size(); ++i)
    cout << ipq.top() << ' '; // 9 9 9 9 9 9 9 9 9
  cout << endl;

  while (!ipq.empty()) {
    cout << ipq.top() << ' '; // 9 8 5 4 3 3 2 1 0
    ipq.pop();
  }
  cout << endl;
  return 0;
}
```

在LeetCode中碰到过几次使用`priority_queue`的题了。
