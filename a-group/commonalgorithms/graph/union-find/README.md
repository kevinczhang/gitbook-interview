# Union Find

**并查集**: 一种用来解决集合**查询**/**合并**的数据结构 支持O(1) find / O(1) union操作

A very good source for Union Find:

Princeton CS Algorithms 4th Edition: [https://algs4.cs.princeton.edu/15uf/](https://algs4.cs.princeton.edu/15uf/)

**Union Find**: 一种用于支持集合**快速合并**和**查找**操作的**数据结构**

* O(1)合并两个集合- Union
* O(1)查询元素所属集合- Find

**基本数据结构**是：使用**哈希表**或者**数组**来存储每个**节点**的**父亲节点**

## 并查集可以干什么? What Union Find Can Do?

1. 判断在不在同一个集合中
   * find 操作
2. 关于集合合并
   * union 操作

**并查集应用场景总结：**

1.合并两个集合

2.查询某个元素所在集合

3.判断两个元素是否在同一个集合

4.获得某个集合的元素个数

5.统计当前集合个数

## 并查集完整模板 Union Find Template

### HashMap Based

```java
class UnionFind {
    UnionFind() {}
    HashMap<Integer, Integer> father = new HashMap<Integer. Integer>();
    int find(int x) {
        int parent = x;
        while (parent ! = father.get(parent)) {
            parent = father.get(parent);
        }
        return parent;
    }
    void union(int x, int y) {
        int fa_x = find(x);
        int fa_y = find(y);
        if (fa_x != fa_y) {
            father.put(fa_x, fa_y);
        }
    }
}
```

### Array Based

#### Another Weighted + Path Compression - Simpler Version

```java
public class UnionFind {
    // 连通分量个数
    private int count;
    // 存储⼀棵树
    private int[] parent;
    // 记录树的「重量」
    private int[] size;
    
    // n 为图中节点的个数
    public UF(int n) {
        this.count = n;
        parent = new int[n];
        size = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
            size[i] = 1;
        }
    }
    
    // 将节点 p 和节点 q 连通
    public void union(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        if (rootP == rootQ)
        return;
        // ⼩树接到⼤树下⾯，较平衡
        if (size[rootP] > size[rootQ]) {
            parent[rootQ] = rootP;
            size[rootP] += size[rootQ];
        } else {
            parent[rootP] = rootQ;
            size[rootQ] += size[rootP];
        }
        // 两个连通分量合并成⼀个连通分量
        count--;
    }
    
    // 判断节点 p 和节点 q 是否连通
    public boolean connected(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        return rootP == rootQ;
    }
    
    // 返回节点 x 的连通分量根节点
    private int find(int x) {
        while (parent[x] != x) {
            // 进⾏路径压缩
            parent[x] = parent[parent[x]];
            x = parent[x];
        }
        return x;
    }
    
    // 返回图中的连通分量个数
    public int count() {
        return count;
    }
}
```

Another temple without rank

```java
class UF {
    // 连通分量个数
    private int count;
    // 存储每个节点的⽗节点
    private int[] parent;
    
    // n 为图中节点的个数
    public UF(int n) {
        this.count = n;
        parent = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }
    
    // 将节点 p 和节点 q 连通
    public void union(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        if (rootP == rootQ)
            return;
        parent[rootQ] = rootP;
        // 两个连通分量合并成⼀个连通分量
        count--;
    }
    
    // 判断节点 p 和节点 q 是否连通
    public boolean connected(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        return rootP == rootQ;
    }
    
    public int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);
        }
        return parent[x];
    }
        
    // 返回图中的连通分量个数
    public int count() {
        return count;
    }
}
```
