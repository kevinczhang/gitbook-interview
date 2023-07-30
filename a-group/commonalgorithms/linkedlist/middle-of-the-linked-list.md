# Middle of the Linked List

Given the `head`of a singly linked list, return _the middle node of the linked list_.

If there are two middle nodes, return **the second middle** node.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

<pre><code>Input: head = [1,2,3,4,5]
<strong>Output:
</strong> [3,4,5]
<strong>Explanation:
</strong> The middle node of the list is node 3.
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)

<pre><code>Input: head = [1,2,3,4,5,6]
<strong>Output:
</strong> [4,5,6]
<strong>Explanation:
</strong> Since the list has two middle nodes with values 3 and 4, we return the second one.
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the list is in the range `[1, 100]`.
* `1 <= Node.val <= 100`

### If there are two middle nodes, return the second middle node.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```

### If there are two middle nodes, return the first middle node.

```java
public ListNode findMiddle(ListNode head) {
    ListNode fast = head;
    ListNode slow = head.next;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```
