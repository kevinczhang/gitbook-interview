# LRU Cache



Design a data structure that follows the constraints of a [**Least Recently Used (LRU) cache**](https://en.wikipedia.org/wiki/Cache\_replacement\_policies#LRU).

Implement the `LRUCache` class:

* `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
* `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
* `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

&#x20;

**Example 1:**

```
Input
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
```

&#x20;

**Constraints:**

* `1 <= capacity <= 3000`
* `0 <= key <= 104`
* `0 <= value <= 105`
* At most 2 `* 105` calls will be made to `get` and `put`.

## Solution 1

```java
class LRUCache {
    int cap;
    LinkedHashMap<Integer, Integer> cache = new LinkedHashMap<>();
    public LRUCache(int capacity) {
        this.cap = capacity;
    }

    public int get(int key) {
        if (!cache.containsKey(key)) {
            return -1;
        }
        // 将 key 变为最近使用
        makeRecently(key);
        return cache.get(key);
    }

    public void put(int key, int val) {
        if (cache.containsKey(key)) {
            // 修改 key 的值
            cache.put(key, val);
            // 将 key 变为最近使用
            makeRecently(key);
            return;
        }

        if (cache.size() >= this.cap) {
            // 链表头部就是最久未使用的 key
            int oldestKey = cache.keySet().iterator().next();
            cache.remove(oldestKey);
        }
        // 将新的 key 添加链表尾部
        cache.put(key, val);
    }

    private void makeRecently(int key) {
        int val = cache.get(key);
        // 删除 key，重新插入到队尾
        cache.remove(key);
        cache.put(key, val);
    }
}


/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

## Solution 2

```java
class LRUCache {
    // key -> Node(key, val)
    private HashMap<Integer, Node> map;
    // Node(k1, v1) <-> Node(k2, v2)...
    private DoubleList cache;
    // 最⼤容量
    private int cap;
    public LRUCache(int capacity) {
        this.cap = capacity;
        map = new HashMap<>();
        cache = new DoubleList();
    }
    
    public int get(int key) {
        if (!map.containsKey(key)) {
            return -1;
        }
        // 将该数据提升为最近使⽤的
        makeRecently(key);
        return map.get(key).val;
    }
    
    public void put(int key, int val) {
        if (map.containsKey(key)) {
            // 删除旧的数据
            deleteKey(key);
            // 新插⼊的数据为最近使⽤的数据
            addRecently(key, val);
            return;
        }
        if (cap == cache.size()) {
            // 删除最久未使⽤的元素
            removeLeastRecently();
        }
        // 添加为最近使⽤的元素
        addRecently(key, val);
    }
    
    /* 将某个 key 提升为最近使⽤的 */
    private void makeRecently(int key) {
        Node x = map.get(key);
        // 先从链表中删除这个节点
        cache.remove(x);
        // 重新插到队尾
        cache.addLast(x);
    }
    /* 添加最近使⽤的元素 */
    private void addRecently(int key, int val) {
        Node x = new Node(key, val);
        // 链表尾部就是最近使⽤的元素
        cache.addLast(x);
        // 别忘了在 map 中添加 key 的映射
        map.put(key, x);
    }
    
    /* 删除某⼀个 key */
    private void deleteKey(int key) {
        Node x = map.get(key);
        // 从链表中删除
        cache.remove(x);
        // 从 map 中删除
        map.remove(key);
    }
    /* 删除最久未使⽤的元素 */
    private void removeLeastRecently() {
        // 链表头部的第⼀个元素就是最久未使⽤的
        Node deletedNode = cache.removeFirst();
        // 同时别忘了从 map 中删除它的 key
        int deletedKey = deletedNode.key;
        map.remove(deletedKey);
    }
}

class Node {
    public int key, val;
    public Node next, prev;
    public Node(int k, int v) {
        this.key = k;
        this.val = v;
    }
}

class DoubleList {
    // 头尾虚节点
    private Node head, tail;
    // 链表元素数
    private int size;
    public DoubleList() {
        // 初始化双向链表的数据
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
        size = 0;
    }
    // 在链表尾部添加节点 x，时间 O(1)
    public void addLast(Node x) {
        x.prev = tail.prev;
        x.next = tail;
        tail.prev.next = x;
        tail.prev = x;
        size++;
    }
    // 删除链表中的 x 节点（x ⼀定存在）
    // 由于是双链表且给的是⽬标 Node 节点，时间 O(1)
    public void remove(Node x) {
        x.prev.next = x.next;
        x.next.prev = x.prev;
        size--;
    }
    // 删除链表中第⼀个节点，并返回该节点，时间 O(1)
    public Node removeFirst() {
        if (head.next == tail)
            return null;
        Node first = head.next;
        remove(first);
        return first;
    }
    // 返回链表⻓度，时间 O(1)
    public int size() { return size; }
}


/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

## Solution 3

```java
public class LRUCache {
    class DoubleLinkedListNode {
	int val, key;
           DoubleLinkedListNode pre, post;

	    public DoubleLinkedListNode(int key, int value) {
		    this.val = value;
		    this.key = key;
	    }
    };
    
    Map<Integer, LRUCache.DoubleLinkedListNode> table;
    DoubleLinkedListNode head, end;
    int capacity, len;
	
    public LRUCache(int capacity) {
        this.table = new HashMap<Integer, LRUCache.DoubleLinkedListNode>();
        this.capacity = capacity;
	this.len = 0;
    }
    
    public int get(int key) {
        if (!table.containsKey(key)) return -1;
		removeNode(table.get(key));
		setHead(table.get(key));
		return table.get(key).val;
    }
    
    public void put(int key, int value) {
        if(table.containsKey(key)){
            DoubleLinkedListNode cur = table.get(key);
            cur.val = value;
            removeNode(cur);         
            setHead(cur);
        } else {
            DoubleLinkedListNode cur = new DoubleLinkedListNode(key,value);
            if(len < capacity){
                setHead(cur);
                table.put(key,cur);
                len++;
            } else {
            	table.remove(end.key);
                end = end.pre;
                if(end != null)
                    end.post = null;
                setHead(cur);
                table.put(key,cur);
            }
        }
    }
    
    void removeNode(DoubleLinkedListNode node){
		DoubleLinkedListNode cur = node, pre = cur.pre, post = cur.post;
		// Link to pre
        if(pre != null){
            pre.post = post;
        } else {
        	head = post;
        }
        // Link to post
        if(post != null){
            post.pre = pre;
        } else {
        	end = pre;
        }
    }
	
    void setHead(DoubleLinkedListNode node){
    	node.post = head;
	node.pre = null;
	if(head != null) head.pre = node; // check head
	if(end == null)	end = node; // check end
	head = node;
    }
}
```
