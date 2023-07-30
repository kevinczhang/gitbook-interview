# Intersection of Two Linked Lists

Given the heads of two singly linked-lists `headA` and `headB`, return _the node at which the two lists intersect_. If the two linked lists have no intersection at all, return `null`.

For example, the following two linked lists begin to intersect at node `c1`:

![](https://assets.leetcode.com/uploads/2021/03/05/160\_statement.png)

The test cases are generated such that there are no cycles anywhere in the entire linked structure.

**Note** that the linked lists must **retain their original structure** after the function returns.

**Custom Judge:**

The inputs to the **judge** are given as follows (your program is **not** given these inputs):

* `intersectVal` - The value of the node where the intersection occurs. This is `0` if there is no intersected node.
* `listA` - The first linked list.
* `listB` - The second linked list.
* `skipA` - The number of nodes to skip ahead in `listA` (starting from the head) to get to the intersected node.
* `skipB` - The number of nodes to skip ahead in `listB` (starting from the head) to get to the intersected node.

The judge will then create the linked structure based on these inputs and pass the two heads, `headA` and `headB` to your program. If you correctly return the intersected node, then your solution will be **accepted**.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/05/160\_example\_1\_1.png)

<pre><code>Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
<strong>Output:
</strong> Intersected at '8'
<strong>Explanation:
</strong> The intersected node's value is 8 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,6,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/05/160\_example\_2.png)

<pre><code>Input: intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
<strong>Output:
</strong> Intersected at '2'
<strong>Explanation:
</strong> The intersected node's value is 2 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [1,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
</code></pre>

**Example 3:**

![](https://assets.leetcode.com/uploads/2021/03/05/160\_example\_3.png)

<pre><code>Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
<strong>Output:
</strong> No intersection
<strong>Explanation:
</strong> From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
</code></pre>

&#x20;

**Constraints:**

* The number of nodes of `listA` is in the `m`.
* The number of nodes of `listB` is in the `n`.
* `1 <= m, n <= 3 * 104`
* `1 <= Node.val <= 105`
* `0 <= skipA < m`
* `0 <= skipB < n`
* `intersectVal` is `0` if `listA` and `listB` do not intersect.
* `intersectVal == listA[skipA] == listB[skipB]` if `listA` and `listB` intersect.

&#x20;

**Follow up:** Could you write a solution that runs in `O(m + n)` time and use only `O(1)` memory?

## Solution

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        // p1 指向 A 链表头结点，p2 指向 B 链表头结点
        ListNode p1 = headA, p2 = headB;
        while (p1 != p2) {
            // p1 走一步，如果走到 A 链表末尾，转到 B 链表
            if (p1 == null) p1 = headB;
            else            p1 = p1.next;
            // p2 走一步，如果走到 B 链表末尾，转到 A 链表
            if (p2 == null) p2 = headA;
            else            p2 = p2.next;
        }
        return p1;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=160

```
