# Queue

> Queue 是一种先进先出(FIFO)的数据结构

## **队列操作 Operations of Queue:**

`enqueue` and `dequeue`

> The **insert** operation is also called **enqueue** and the new element is always `added at the end of the queue`.
>
> The **delete** operation is called **dequeue**. You are only allowed to `remove the first element`.

## Queue Implementation

### Queue Using Array

#### Circular Queue

Use a **fixed-size array** and **two pointers** to indicate the starting position and the ending position. And the goal is to **reuse** the **wasted** **storage** we mentioned previously.

### Queue using Linked List

## Monotonic Queue

```java
/* 单调队列的实现 */
class MonotonicQueue {
    LinkedList<Integer> maxq = new LinkedList<>();
    public void push(int n) {
        // 将小于 n 的元素全部删除
        while (!maxq.isEmpty() && maxq.getLast() < n) {
            maxq.pollLast();
        }
        // 然后将 n 加入尾部
        maxq.addLast(n);
    }

    public int max() {
        return maxq.getFirst();
    }

    public void pop(int n) {
        if (n == maxq.getFirst()) {
            maxq.pollFirst();
        }
    }
}
```
