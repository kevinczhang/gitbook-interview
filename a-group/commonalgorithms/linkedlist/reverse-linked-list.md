# Reverse Linked List

Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

<pre><code>Input: head = [1,2,3,4,5]
<strong>Output:
</strong> [5,4,3,2,1]
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

<pre><code>Input: head = [1,2]
<strong>Output:
</strong> [2,1]
</code></pre>

**Example 3:**

<pre><code>Input: head = []
<strong>Output:
</strong> []
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the list is the range `[0, 5000]`.
* `-5000 <= Node.val <= 5000`

&#x20;

**Follow up:** A linked list can be reversed either iteratively or recursively. Could you implement both?

## Recursive Solution

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        
        ListNode reversed = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return reversed;
    }
}
```

## Iterative Solution

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null)
            return head;
        ListNode cur = head;
        while (cur.next != null) {
            ListNode newHead = cur.next;
            cur.next = newHead.next;
            newHead.next = head;
            head = newHead;
        }
        return head;
    }
}
```
