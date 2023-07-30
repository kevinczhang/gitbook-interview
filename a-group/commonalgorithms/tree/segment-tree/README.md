# Segment Tree

Source: Jiuzhang's Tutorial: [https://www.jiuzhang.com/tutorial/segment-tree/](https://www.jiuzhang.com/tutorial/segment-tree/)

**Segment Tree** (a.k.a Interval Tree) is an advanced data structure which can support queries like:

* which of these intervals contain a given point
* which of these points are in a given interval

See wiki:

* [Segment Tree](https://en.wikipedia.org/wiki/Segment\_tree)
* [Interval Tree](https://en.wikipedia.org/wiki/Interval\_tree)

The structure of Segment Tree is a binary tree which each node has two attributes start and end denote an segment / interval.

start and end are both integers, they should be assigned in following rules:

* The root's start and end is given by build method.
* The left child of node A has start=A.left, end=(A.left + A.right) / 2.
*   The right child of node A has start=(A.left + A.right) / 2 + 1, end=A.right.

    if start equals to end, there will be no children for this node.
* Implement a build method with two parameters start and end, so that we can create a corresponding segment tree with every node has the correct start and end value, return the root of this segment tree.

Example\
Given start=0, end=3. The segment tree will be:

```
               [0,  3]
             /        \
      [0,  1]           [2, 3]
      /     \           /     \
   [0, 0]  [1, 1]     [2, 2]  [3, 3]
```

Given start=1, end=6. The segment tree will be:

```
               [1,  6]
             /        \
      [1,  3]           [4,  6]
      /     \           /     \
   [1, 2]  [3,3]     [4, 5]   [6,6]
   /    \           /     \
[1,1]   [2,2]     [4,4]   [5,5]
```

## 1. 线段树可以解决什么问题

**线段树是什么？**

线段树是一种高级数据结构，也是一种树结构，准确的说是二叉树。它能够高效的处理区间修改查询等问题。因此学习线段树，我们就是在学习一种全新的高级数据结构，学习它如何组织数据，然后高效的进行数据查询，修改等操作。

**线段树树的基本操作有哪些？**

1.  线段树的构建

    [http://www.lintcode.com/en/problem/segment-tree-build/](http://www.lintcode.com/en/problem/segment-tree-build/)
2.  线段树的修改

    [http://www.lintcode.com/en/problem/segment-tree-modify/](http://www.lintcode.com/en/problem/segment-tree-modify/)
3.  线段树的查询

    [http://www.lintcode.com/en/problem/segment-tree-query/](http://www.lintcode.com/en/problem/segment-tree-query/)

**线段树有什么用？**

另外，在一些不一定要用线段树解决的问题中，线段树可以帮助大家降低问题的难度，虽然这些问题`不是直接考线段树`，但是如果你会线段树，那么用线段树去解决就会变得特别容易，降低你的`思维复杂度`，`coding的复杂度`。不仅仅是线段树，学习其他高级数据结构如平衡树，都可以帮你简化一些问题思考和coding复杂度，这也是学习高级数据结构的好处和用处。

**线段树问题举例**

我们有时会遇到这样的问题: 给你一些数，组成一个序列，如`[1 4 2 3]`,有两种操做:\
操作一:给序列的第i个数加上X (X可以为负数)\
操作二:询问序列中最大的数是什么? 格式`query(start, end)`，表示区间`[start, end]`内，最大值是多少？

## 2. 线段树的结构

### 第一节：什么是线段树，它长什么样？

首先线段树是一棵`二叉树`, 平常我们所指的线段树都是指**一维线段树**。 故名思义, 线段树能解决的是线段上的问题, 这个线段也可指`区间`.\
我们先来看**线段树的逻辑结构**。

一颗线段树的构造就是根据区间的性质的来构造的, 如下是一棵区间`[0, 3]`的线段树，每个`[start, end]`都是一个二叉树中的节点。

```
          [0,3]
         /     \
    [0,1]       [2,3]
    /   \       /   \
 [0,0] [1,1] [2,2] [3,3]
```

区间划分大概就是上述的区间划分。可以看出每次都将区间的长度一分为二,数列长度为n,所以线段树的高度是`log(n)`,这是很多高效操作的基础。\
上述的区间存储的只是区间的左右边界。我们可以将区间的最大值加入进来,也就是树中的Node需要存储left，right左右子节点外，还需要存储`start, end, val`区间的范围和区间内表示的值。

```
            [0,3]
           (val=4)
         /         \
     [0,1]         [2,3]
    (val=4)       (val=3)
    /    \         /    \
 [0,0]  [1,1]   [2,2]  [3,3]
(val=1)(val=4) (val=2)(val=3)
```

区间的第三维就是区间的最大值。

加这一维的时候只需要在建完了左右区间之后，根据左右区间的最大值来更新当前区间的最大值即可，即当前子树的最大值是左子树的最大和右子树的最大值里面选出来的最大值。

因为每次将区间的长度一分为二,所有创造的节点个数，即底层有n个节点，那么倒数第二次约n/2个节点，倒数第三次约n/4个节点，依次类推：

```
    n + 1/2 * n + 1/4 * n + 1/8 * n + ...
=   (1 + 1/2 + 1/4 + 1/8 + ...) * n
=   2n
```

`所以构造线段树的时间复杂度和空间复杂度都为O(n)`

### 第二节：线段树中的Node如何定义

二叉树的节点区间定义，`[start, end]`代表节点的区间范围，max 是节点在\[start, end]区间上的最大值 left , right 是当前节点区间划分之后的左右节点区间

```java
// 节点区间定义
// [start, end] 代表节点的区间范围
// max 是节点在(start,end)区间上的最大值
// left , right 是当前节点区间划分之后的左右节点区间
public class SegmentTreeNode {
    public int start, end, max;
    public SegmentTreeNode left, right;
    public SegmentTreeNode(int start, int end, int max) {
        this.start = start;
        this.end = end;
        this.max = max
        this.left = this.right = null;
    }
}
```

## 3. 线段树区间最大值维护

给定一个区间，我们要维护线段树中存在的区间中最大的值。这将有利于我们高效的查询任何区间的最大值。给出A数组，基于A数组构建一棵维护最大值的线段树，我们可以在`O(logN)`的复杂度内查询任意区间的最大值：

比如原数组`A = [1, 4, 2, 3]`

```
            [0,3]
           (val=4)
         /         \
     [0,1]         [2,3]
    (val=4)       (val=3)
    /    \         /    \
 [0,0]  [1,1]   [2,2]  [3,3]
(val=1)(val=4) (val=2)(val=3)
```

#### Build Segment Tree

**build()**

```java
// 构造的代码及注释
public SegmentTreeNode build(int[] A) {
    // write your code here
    return buildhelper(0, A.length - 1, A);
}
```

**buildHelper()**

```java
public SegmentTreeNode buildhelper(int left, int right, int[] A){
    if(left > right){
        return null;
    }
    SegmentTreeNode root = new SegmentTreeNode(left, right, A[left]); // 根据节点区间的左边界的序列值为节点赋初值
    if(left == right){
        return root; // 如果左边界和右边界相等,节点左边界的序列值就是线段树节点的接节点值
    }
    int mid = (left + right) / 2; // 划分当前区间的左右区间
    root.left = buildhelper(left, mid, A);
    root.right = buildhelper(mid + 1, right, A);
    root.max = Math.max(root.left.max, root.right.max); // 根据节点区间的左右区间的节点值得到当前节点的节点值
    return root;
}
```

**举一反三：**\
如果需要区间的最小值:\
`root.min = Math.min(root.left.min, root.right.min);`\
如果需要区间的和:\
`root.sum = root.left.sum + root.right.sum;`

## 4.线段树的区间查询

### 4.1. 如何更好的查询Query

构造线段树的目的就是为了更快的查询。

给定一个区间，要求区间中最大的值。线段树的`区间查询操作`就是将当前区间`分解为较小的子区间`，然后由子区间的最大值就可以快速得到需要查询区间的最大值。

```
            [0,3]
           (val=4)
         /         \
     [0,1]         [2,3]
    (val=4)       (val=3)
    /    \         /    \
 [0,0]  [1,1]   [2,2]  [3,3]
(val=1)(val=4) (val=2)(val=3)
```

`query(1,3) = max(query(1,1), query(2,3)) = max(4,3) = 4`

上述例子将`[1, 3]`区间分为了`[1, 1]`和`[2, 3]`两个区间,因为`[1, 1]`和`[2, 3]`存在于线段树上，所以区间的最大值已经记录好了，所以直接拿来用就可以了。所以拆分区间的目的是划分成为`线段树上已经存在的小线段`。

### 4.2. 如何拆分区间变成线段树上有的小区间：

在线段树的层数上考虑查询 考虑长度为8的序列构造成的线段树区间\[1, 8], 现在我们查询区间\[1, 7]。

第一层会查询试图查询`[1, 7]`, 发现区间不存在，然后根据mid位置拆分`[1, 4]`和`[5, 7]`\
第二层会查询`[1, 4]`,`[5, 7]`, 发现`[1, 4]`已经存在，返回即可，`[5, 7]`仍旧需要继续拆分\
第三层会查询`[5, 6]`,`[7, 7]`, 发现`[5, 6]`已经存在，返回即可，`[7, 7]`仍旧需要继续拆分\
第四层会查询`[7, 7]`

任意长度的线段，最多被拆分成`logn`条线段树上存在的线段，所以查询的时间复杂度为`O(log(n))` 记住就好：）

```java
// 区间查询的代码及注释
public int query(TreeNode root, int start, int end) {
    if (start <= root.start && root.end <= end) {
        // 如果查询区间在当前节点的区间之内,直接输出结果
        return root.max;
    }
    int mid = (root.start + root.end) / 2; // 将当前节点区间分割为左右2个区间的分割线
    int ans = Integer.MIN_VALUE; // 给结果赋初值
    if (mid >= start) {   // 如果查询区间和左边节点区间有交集,则寻找查询区间在左边区间上的最大值
        ans = Math.max(ans, query(root.left, start, end));
    }
    if (mid + 1 <= end) { // 如果查询区间和右边节点区间有交集,则寻找查询区间在右边区间上的最大值
        ans = Math.max(ans, query(root.right, start, end));
    }
    return ans; // 返回查询结果
}
```

## 5. 线段树的单点更新

### 更新序列中的一个点

```
            [0,3]
           (val=4)
         /         \
     [0,1]         [2,3]
    (val=4)       (val=3)
    /    \         /    \
 [0,0]  [1,1]   [2,2]  [3,3]
(val=1)(val=4) (val=2)(val=3)
```

更新序列中的一个节点，如何把这种变化体现到线段树中去，例如，将序列中的第4个点A\[3]更新为5, 要变动3个区间中的值,分别为\[3,3],\[2,3],\[0,3]

`提问：为什么需要更新这三个区间？`：因为只有这三个在线段树中的区间，覆盖了3这个点。

```
            [0,3]
           (val=5)
         /         \
     [0,1]         [2,3]
    (val=4)       (val=5)
    /    \         /    \
 [0,0]  [1,1]   [2,2]  [3,3]
(val=1)(val=4) (val=2)(val=5)
```

可以这样想,改动一个节点,与这个节点对应的叶子节点需要变动。因为叶子节点的值的改变可能影响到父亲节点，然后叶子节点的父亲节点也可能需要变动。

`如果我们继续把A[2]从2变成4，线段树又该如何更新呢？`\
线段树变化后的状态为：

```
            [0,3]
           (val=5)
         /         \
     [0,1]         [2,3]
    (val=4)       (val=5)
    /    \         /    \
 [0,0]  [1,1]   [2,2]  [3,3]
(val=1)(val=4) (val=4)(val=5)
```

`如果我们继续把A[1]从4变成3，线段树又该如何更新呢？`\
线段树变化后的状态为：

```
            [0,3]
           (val=5)
         /         \
     [0,1]         [2,3]
    (val=3)       (val=5)
    /    \         /    \
 [0,0]  [1,1]   [2,2]  [3,3]
(val=1)(val=3) (val=4)(val=5)
```

更新所以需要从`叶子节点一路走到根节点`, 去更新线段树上的值。因为线段树的高度为log(n),所以更新序列中一个节点的复杂度为log(n)。\
因为每次从父节点走到子节点的时候，区间都是一分为二，那么我们要修改index的时候，我们从root出发，判断index会落在左边还是右边，然后继续递归，这样就可以很容易从根节点走到叶子节点，然后更新叶子节点的值，`递归返回前`不断更新每个节点的最大值即可。具体代码实现如下：

```java
// 单点更新的代码及注释
public void modify(SegmentTreeNode root, int index, int value) {
    // write your code here
    if(root.start == root.end && root.start == index) { // 找到被改动的叶子节点
        root.max = value; // 改变value值
        return ;
    }
    int mid = (root.start + root.end) / 2; // 将当前节点区间分割为2个区间的分割线
    if(index <= mid){ // 如果index在当前节点的左边
        modify(root.left, index, value); // 递归操作
        root.max = Math.max(root.right.max, root.left.max); // 可能对当前节点的影响
    } else {            // 如果index在当前节点的右边
        modify(root.right, index, value); // 递归操作
        root.max = Math.max(root.left.max, root.right.max); // 可能对当前节点的影响
    }
    return ;
}
```

如果需要区间的最小值或者区间的和，构造的时候同理。

## 6.总结 - 线段树问题解决的框架

通过前面问题的分析，我们对线段树问题可以做如下总结：

* 如果问题带有**区间操作**，或者可以**转化**成**区间操作**，可以尝试往线段树方向考虑
  * 从面试官给的题目中抽象问题，将问题转化成一列区间操作，注意这步很关键
* 当我们分析出问题是一些列区间操作的时候，我们都可以采用线段树来解决这个问题
  * **对区间的一个点的值进行修改**
  * **对区间的一段值进行统一的修改**
  * **询问区间的和**
  * **询问区间的最大值、最小值**
* 套用我们前面讲到的经典步骤和写法，即可在面试中完美的解决这些题目！

**什么情况下，无法使用线段树？**

如果我们删除或者增加区间中的元素，那么区间的大小将发生变化，此时是无法使用线段树解决这种问题的。

其他参考资料：

[2004 - 林涛：《线段树的应用》 - 林涛.pdf](http://media.jiuzhang.com/session/2004\_-\_%E6%9E%97%E6%B6%9B%E7%BA%BF%E6%AE%B5%E6%A0%91%E7%9A%84%E5%BA%94%E7%94%A8%E6%9E%97%E6%B6%9B.pdf.pdf)

[浅谈线段树在信息学竞赛中的应用 - 岳云涛](http://media.jiuzhang.com/session/%E6%B5%85%E8%B0%88%E7%BA%BF%E6%AE%B5%E6%A0%91%E5%9C%A8%E4%BF%A1%E6%81%AF%E5%AD%A6%E7%AB%9E%E8%B5%9B%E4%B8%AD%E7%9A%84%E5%BA%94%E7%94%A8-%E5%B2%B3%E4%BA%91%E6%B6%9B.pdf)
