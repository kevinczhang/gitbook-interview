# Sync

1. **synchronized** keyword is used for exclusive accessing.&#x20;
2. To make a **method synchronized**, simply add the synchronized keyword to its declaration. Then no two invocations of synchronized methods on the same object can interleave with each other.&#x20;
3. Synchronized statements must specify the object that provides the intrinsic lock. When **synchronized(this)** is used, you have to avoid to synchronizing invocations of other objects' methods.
4. **wait()** tells the calling thread to give up the monitor and go to sleep until some other thread enters the same monitor and calls **notify( )**. **notify()** wakes up the first thread that called **wait()** on the same object.

## Method synchronized

```java
/**
 * {@code synchronized} ("only let one thread in here at a time".) and 
 * {@code join} ("wait until * thread on which join has called finished") keyword.
 */
public class Worker {

    private int count = 0;

    public static void main(String[] args) {
        Worker worker = new Worker();
        worker.doWork();
    }

    /**
     * Run code again by removing the synchronized and join keywords By removing
     * synchronized keyword count variable will vary that is it is not atomic in
     * this case due to the reason that count is shared between the threads or
     * without join keyword count will output wrong.
     */
    public synchronized void increment(String threadName) throws InterruptedException {
        count++;
        //Thread.sleep(1000);
        System.out.println("Thread in Progress: " + threadName + " and count is: " + count);
    }

    public void doWork() {
        Thread thread1 = new Thread(new Runnable() {
            public void run() {
                for (int i = 0; i < 10; i++) {
                    try {
                        increment(Thread.currentThread().getName());
                    } catch (InterruptedException ex) {
                        Logger.getLogger(Worker.class.getName()).log(Level.SEVERE, null, ex);
                    }
                }
            }
        });
        thread1.start();
        Thread thread2 = new Thread(new Runnable() {
            public void run() {
                for (int i = 0; i < 10; i++) {
                    try {
                        increment(Thread.currentThread().getName());
                    } catch (InterruptedException ex) {
                        Logger.getLogger(Worker.class.getName()).log(Level.SEVERE, null, ex);
                    }
                }
            }
        });
        thread2.start();

        /**
         * Join Threads: Finish until thread finishes execution, then progress
         * the code Reminder: your method is also a thread so without joining
         * threads System.out.println("Count is: " + count); will work
         * immediately. Join does not terminate Thread 2, just progress of the
         * code stops until Threads terminate.
         */
        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException ignored) {}
        System.out.println("Count is: " + count);
    }
}
```

## Synchronized statements

```java
public class Processor {

    private LinkedList<Integer> list = new LinkedList<>();
    private final int LIMIT = 10;
    private final Object lock = new Object();

    public void produce() throws InterruptedException {
        int value = 0;
        while (true) {
            synchronized (lock) {
                //whenever the thread is notified starts again from the loop
                while (list.size() == LIMIT) {
                    lock.wait();// wait() is also true
                }
                list.add(value);

                System.out.println("Producer added: " + value + " queue size is " + list.size());
                value++;
                lock.notify();
            }
        }
    }

    public void consume() throws InterruptedException {
        Random random = new Random();
        while (true) {
            synchronized (lock) {
                while (list.size() == 0) {
                    lock.wait();
                }

                int value = list.removeFirst();
                System.out.print("Removed value by consumer is: " + value);
                System.out.println(" Now list size is: " + list.size());
                lock.notify();
            }
            Thread.sleep(random.nextInt(1000)); //force producer fill the queue to LIMIT_SIZE
        }
    }
}
```
