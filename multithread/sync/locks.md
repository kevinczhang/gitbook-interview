# Locks

1. **Lock**: This is the base interface for Lock API. It provides all the features of synchronized keyword with additional ways to create different Conditions for locking, providing timeout for thread to wait for lock. Some of the important methods are lock() to acquire the lock, unlock() to release the lock, tryLock() to wait for lock for a certain period of time, newCondition() to create the Condition etc.
2. **Condition**: Condition objects are similar to [Object wait-notify](https://www.journaldev.com/1037/java-thread-wait-notify-and-notifyall-example) model with additional feature to create different sets of wait. A Condition object is always created by Lock object. Some of the important methods are await() that is similar to wait() and signal(), signalAll() that is similar to notify() and notifyAll() methods.
3. **ReadWriteLock**: It contains a pair of associated locks, one for read-only operations and another one for writing. The read lock may be held simultaneously by multiple reader threads as long as there are no writer threads. The write lock is exclusive.
4. **ReentrantLock**: This is the most widely used implementation class of Lock interface. This class implements the Lock interface in similar way as synchronized keyword. Apart from Lock interface implementation, ReentrantLock contains some utility methods to get the thread holding the lock, threads waiting to acquire the lock etc.

{% hint style="info" %}
synchronized block are reentrant in nature i.e if a thread has lock on the monitor object and if another synchronized block requires to have the lock on the same monitor object then thread can enter that code block. I think this is the reason for the class name to be ReentrantLock.
{% endhint %}

```java
class BlockingQueue<T> {

    private Queue<T> queue = new LinkedList<>();
    private int capacity;
    private Lock lock = new ReentrantLock();
    //condition variables
    private Condition notFull = lock.newCondition();
    private Condition notEmpty = lock.newCondition();

    public BlockingQueue(int capacity) {
        this.capacity = capacity;
    }

    public void put(T element) throws InterruptedException {
        lock.lock();
        try {
            while (queue.size() == capacity) {
                System.out.println("queue is full cannot put");
                notFull.await(); //releases lock
            }

            queue.add(element);
            System.out.println("Added to the queue " + element);
            notEmpty.signal(); //calls waiting thread on the same object
        } finally {
            lock.unlock();
        }
    }

    public T take() throws InterruptedException {
        lock.lock();
        try {
            while (queue.isEmpty()) {
                System.out.println("queue is empty, cannot take");
                notEmpty.await(); //releases lock
            }

            T item = queue.remove();
            System.out.println("Removed to the queue " + item);
            notFull.signal(); //calls waiting thread on same object
            return item;
        } finally {
            lock.unlock();
        }
    }
}

@SuppressWarnings("InfiniteLoopStatement")
public class BlockingQueueApp {

    public static void main(String[] args) throws InterruptedException {
        final BlockingQueue<Integer> blockingQueue = new BlockingQueue<>(10);
        final Random random = new Random();
        Thread t1 = new Thread(new Runnable() {
            public void run() {
                try {
                    while (true) {
                        blockingQueue.put(random.nextInt(10));
                    }
                } catch (InterruptedException ignored) {}
            }
        });

        Thread t2 = new Thread(new Runnable() {
            public void run() {
                try {
                    Thread.sleep(1000);//wait for putting to the queue first
                } catch (InterruptedException ex) {
                    System.out.println("Exception " + ex.getMessage());
                }
                try {
                    while (true) {
                        blockingQueue.take();
                    }
                } catch (InterruptedException ignored) {}
            }
        });
        t1.start();
        t2.start();
        t1.join();
        t2.join();
    }
}
```
