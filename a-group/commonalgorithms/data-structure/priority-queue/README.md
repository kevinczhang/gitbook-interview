# Priority Queue

## Heap 操作

* **插入:** 将新元素放到`heap[size+1]`的位置每次比较它的它父亲元素，如果小于它的父亲，证明现在不满 足堆的性质，然后向上**Sift Up**
* **删除:** 将根节点和最后一个节点进行交换如果该节点大于其中一个儿子，那么将其与其较小的儿子进行交换做**Sift Down，**&#x76F4;到该节点的儿子均大于它的值，或者它的儿子为空

### Heap

**Interface 接口**\
• O(logN) Push -> Sift Up\
• O(logN) Pop -> Sift Down • O(1) Top\
• O(N) Delete

## Heap Application

> Priority Queue: Priority queues can be efficiently implemented using Binary Heap because it supports insert(), delete() and extractmax(), decreaseKey() operations in O(logn) time.

[https://www.geeksforgeeks.org/binary-heap/](https://www.geeksforgeeks.org/binary-heap/)

## Heap Template

### Priority Queue in Java

[https://stackoverflow.com/questions/6065710/how-does-javas-priorityqueue-differ-from-a-min-heap](https://stackoverflow.com/questions/6065710/how-does-javas-priorityqueue-differ-from-a-min-heap)

> The default **PriorityQueue** is implemented with **Min-Heap**, that is the top element is the minimum one in the heap. In order to implement a max-heap, you can create your own Comparator:

```java
import java.util.Comparator;

public class MyComparator implements Comparator<Integer>
{
    public int compare( Integer x, Integer y )
    {
        return y - x;
    }
}
```

```java
PriorityQueue minHeap = new PriorityQueue(); // default natural ordering; min-heap
PriorityQueue maxHeap = new PriorityQueue(size, new MyComparator());
```

### HashHeap

[https://github.com/awangdev/LintCode/blob/master/Java/HashHeap.java](https://github.com/awangdev/LintCode/blob/master/Java/HashHeap.java)

```java
// HashHeap Implementation

// 接口
// • O(logN) Push -> Sift Up
// • O(logN) Pop -> Sift Down • O(1) Top
// • O(logN) Delete

class HashHeap {
    ArrayList<Integer> heap;
    String mode;
    int size_t;
    HashMap<Integer, Node> hash;

    class Node {
        public Integer id;
        public Integer num;

        Node(Node now) {
            id = now.id;
            num = now.num;
        }

        Node(Integer first, Integer second) {
            this.id = first;
            this.num = second;
        }
    }

    public HashHeap(String mod) {
        // TODO Auto-generated constructor stub
        heap = new ArrayList<Integer>();
        mode = mod;
        hash = new HashMap<Integer, Node>();
        size_t = 0;
    }

    int peak() {
        return heap.get(0);
    }

    int size() {
        return size_t;
    }

    Boolean empty() {
        return (heap.size() == 0);
    }

    int parent(int id) {
        if (id == 0) {
            return -1;
        }
        return (id - 1) / 2;
    }

    int lson(int id) {
        return id * 2 + 1;
    }

    int rson(int id) {
        return id * 2 + 2;
    }

    boolean comparesmall(int a, int b) {
        if (a <= b) {
            if (mode == "min")
                return true;
            else
                return false;
        } else {
            if (mode == "min")
                return false;
            else
                return true;
        }

    }

    void swap(int idA, int idB) {
        int valA = heap.get(idA);
        int valB = heap.get(idB);

        int numA = hash.get(valA).num;
        int numB = hash.get(valB).num;
        hash.put(valB, new Node(idA, numB));
        hash.put(valA, new Node(idB, numA));
        heap.set(idA, valB);
        heap.set(idB, valA);
    }

    Integer poll() {
        size_t--;
        Integer now = heap.get(0);
        Node hashnow = hash.get(now);
        if (hashnow.num == 1) {
            swap(0, heap.size() - 1);
            hash.remove(now);
            heap.remove(heap.size() - 1);
            if (heap.size() > 0) {
                siftdown(0);
            }
        } else {
            hash.put(now, new Node(0, hashnow.num - 1));
        }
        return now;
    }

    void add(int now) {
        size_t++;
        if (hash.containsKey(now)) {
            Node hashnow = hash.get(now);
            hash.put(now, new Node(hashnow.id, hashnow.num + 1));

        } else {
            heap.add(now);
            hash.put(now, new Node(heap.size() - 1, 1));
        }

        siftup(heap.size() - 1);
    }

    void delete(int now) {
        size_t--;
        ;
        Node hashnow = hash.get(now);
        int id = hashnow.id;
        int num = hashnow.num;
        if (hashnow.num == 1) {

            swap(id, heap.size() - 1);
            hash.remove(now);
            heap.remove(heap.size() - 1);
            if (heap.size() > id) {
                siftup(id);
                siftdown(id);
            }
        } else {
            hash.put(now, new Node(id, num - 1));
        }
    }

    void siftup(int id) {
        while (parent(id) > -1) {
            int parentId = parent(id);
            if (comparesmall(heap.get(parentId), heap.get(id)) == true) {
                break;
            } else {
                swap(id, parentId);
            }
            id = parentId;
        }
    }

    void siftdown(int id) {
        while (lson(id) < heap.size()) {
            int leftId = lson(id);
            int rightId = rson(id);
            int son;
            if (rightId >= heap.size() || (comparesmall(heap.get(leftId), heap.get(rightId)) == true)) {
                son = leftId;
            } else {
                son = rightId;
            }
            if (comparesmall(heap.get(id), heap.get(son)) == true) {
                break;
            } else {
                swap(id, son);
            }
            id = son;
        }
    }
}
```

## Heap Definition

(Binary) **Heap** is a special case of **balanced** **binary** **tree** data structure where the **root-node key** is compared with its **children** and arranged accordingly.

**Min-Heap** − Where the value of the root node is less than or equal to either of its children.

**Max-Heap** − Where the value of the root node is greater than or equal to either of its children.

[https://www.tutorialspoint.com/data\_structures\_algorithms/heap\_data\_structure.htm](https://www.tutorialspoint.com/data_structures_algorithms/heap_data_structure.htm)

## Heap Construction

### Max Heap Construction Algorithm

```
Step 1 − Create a new node at the end of heap.
Step 2 − Assign new value to the node.
Step 3 − Compare the value of this child node with its parent.
Step 4 − If value of parent is less than child, then swap them.
Step 5 − Repeat step 3 & 4 until Heap property holds.
```

**Note** − In **Min Heap** construction algorithm, we expect the value of the parent node to be less than that of the child node.

### Max Heap Deletion Algorithm

Deletion in Max (or Min) Heap always happens at the root to remove the Maximum (or minimum) value.

```
Step 1 − Remove root node.
Step 2 − Move the last element of last level to root.
Step 3 − Compare the value of this child node with its parent.
Step 4 − If value of parent is less than child, then swap them.
Step 5 − Repeat step 3 & 4 until Heap property holds.
```

## Reference

\[Heap Data Structures]\([https://www.tutorialspoint.com/data\_structures\_algorithms/heap\_data\_structure.htm\\](https://www.tutorialspoint.com/data_structures_algorithms/heap_data_structure.htm\)/)

\[GeeksforGeeks]\([https://www.geeksforgeeks.org/binary-heap/\\](https://www.geeksforgeeks.org/binary-heap/\)/)

\[HackerRank Heaps]\([https://www.hackerrank.com/topics/heaps](https://www.hackerrank.com/topics/heaps\)\)/)

PriorityQueue: [https://algs4.cs.princeton.edu/24pq/](https://algs4.cs.princeton.edu/24pq/)
