# Copy List with Random Pointer

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    /**
     * @param head: The head of linked list with a random pointer.
     * @return: A new head of a deep copy of the list.
     */
    public RandomListNode copyRandomList(RandomListNode head) {
        if(head == null) return null;
	      // Weave new node into the list
        RandomListNode cur = head;
        while(cur != null){
            RandomListNode newNode = new RandomListNode(cur.label);
            RandomListNode nextNode = cur.next;
            cur.next = newNode;
            newNode.next = nextNode;
            cur = nextNode;
        }
        // Link random point
        cur = head;
        while(cur != null){
            if(cur.random != null){
                cur.next.random = cur.random.next;
            }
            cur = cur.next.next;
        }
        // Break new list from the whole list
        RandomListNode newHead = head.next;
        RandomListNode newCur = newHead;
        head.next = newCur.next;
        cur = head.next;
        while(cur != null){
            newCur.next = cur.next;
            cur.next = cur.next.next;
            cur = cur.next;
            newCur = newCur.next;
        }
        return newHead;
    }
}

```
