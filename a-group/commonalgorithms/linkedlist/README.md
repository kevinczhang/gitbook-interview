# LinkedList

### Merge Two Sorted Lists

Iterative

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode lastNode = dummy;

    while (l1 != null && l2 != null) {
        if (l1.val < l2.val) {
            lastNode.next = l1;
            l1 = l1.next;
        } else {
            lastNode.next = l2;
            l2 = l2.next;
        }
        lastNode = lastNode.next;
    }

    if (l1 != null) {
        lastNode.next = l1;
    } else {
        lastNode.next = l2;
    }

    return dummy.next;
}
```

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode p = dummy;
        while (l1 != null || l2 != null) {
            if (l1 == null) {
                p.next = l2;
                break;
            }
            if (l2 == null) {
                p.next = l1;
                break;
            }
            if (l1.val < l2.val) {
                p.next = l1;
                l1 = l1.next;
            } else {
                p.next = l2;
                l2 = l2.next;
            }
            p = p.next;
        }
        return dummy.next;
    }
}
```

Recursive

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    if (l1 == null) return l2;
    if (l2 == null) return l1;
    if (l1.val < l2.val) {
        l1.next = mergeTwoLists(l1.next, l2);
        return l1;
    } else {
        l2.next = mergeTwoLists(l1, l2.next);
        return l2;
    }
}
```

### Remove Linked List Elements

Remove all elements from a linked list of integers that have value val.

Iterative

```java
public ListNode removeElements(ListNode head, int val) {
   ListNode dummy = new ListNode(0);
   dummy.next = head;
   ListNode curr = head;
   ListNode prev = dummy;
   while (curr != null) {
      if (curr.val == val) {
           prev.next = curr.next; 
      } else {
           prev = prev.next;
      }  
      curr = curr.next;
   }
   return dummy.next;
}
```

Recursive

```java
public ListNode removeElements(ListNode head, int val) {
        if (head == null) return null;
        head.next = removeElements(head.next, val);
        return head.val == val ? head.next : head;
}
```

### Linked List Has Cycle

```java
public Boolean hasCycle(ListNode head) {
    if (head == null || head.next == null) {
        return false;
    }

    ListNode fast, slow;
    fast = head.next;
    slow = head;
    while (fast != slow) {
        if(fast==null || fast.next==null)
            return false;
        fast = fast.next.next;
        slow = slow.next;
    }
    return true;
}
```
