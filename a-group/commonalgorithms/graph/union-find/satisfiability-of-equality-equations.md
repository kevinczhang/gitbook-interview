# Satisfiability of Equality Equations

You are given an array of strings `equations` that represent relationships between variables where each string `equations[i]` is of length `4` and takes one of two different forms: `"xi==yi"` or `"xi!=yi"`.Here, `xi` and `yi` are lowercase letters (not necessarily different) that represent one-letter variable names.

Return `true` _if it is possible to assign integers to variable names so as to satisfy all the given equations, or_ `false` _otherwise_.

&#x20;

**Example 1:**

<pre><code>Input: equations = ["a==b","b!=a"]
<strong>Output:
</strong> false
<strong>Explanation:
</strong> If we assign say, a = 1 and b = 1, then the first equation is satisfied, but not the second.
There is no way to assign the variables to satisfy both equations.
</code></pre>

**Example 2:**

<pre><code>Input: equations = ["b==a","a==b"]
<strong>Output:
</strong> true
<strong>Explanation:
</strong> We could assign a = 1 and b = 1 to satisfy both equations.
</code></pre>

&#x20;

**Constraints:**

* `1 <= equations.length <= 500`
* `equations[i].length == 4`
* `equations[i][0]` is a lowercase letter.
* `equations[i][1]` is either `'='` or `'!'`.
* `equations[i][2]` is `'='`.
* `equations[i][3]` is a lowercase letter.

```java
class Solution {
    public boolean equationsPossible(String[] equations) {
        // 26 个英⽂字⺟
        UF uf = new UF(26);
        // 先让相等的字⺟形成连通分量
        for (String eq : equations) {
            if (eq.charAt(1) == '=') {
                char x = eq.charAt(0);
                char y = eq.charAt(3);
                uf.union(x - 'a', y - 'a');
            }
        }
        // 检查不等关系是否打破相等关系的连通性
        for (String eq : equations) {
            if (eq.charAt(1) == '!') {
                char x = eq.charAt(0);
                char y = eq.charAt(3);
                // 如果相等关系成⽴，就是逻辑冲突
                if (uf.connected(x - 'a', y - 'a'))
                    return false;
            }
        }
        return true;
    }
}

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
