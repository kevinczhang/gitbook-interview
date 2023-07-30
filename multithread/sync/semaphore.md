---
description: A semaphore controls access to a shared resource through the use of a counter.
---

# Semaphore

If the counter is greater than zero, then access is allowed. If it is zero, then access is denied. What the counter is counting are permits that allow access to the shared resource. Thus, to access the resource, a thread must be granted a permit from the semaphore.

* If the semaphore’s count is greater than zero, then the thread acquires a permit, which causes the semaphore’s count to be decremented.
* Otherwise, the thread will be blocked until a permit can be acquired.
* When the thread no longer needs an access to the shared resource, it releases the permit, which causes the semaphore’s count to be incremented.
* If there is another thread waiting for a permit, then that thread will acquire a permit at that time.

```java
public class App {

    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newCachedThreadPool();

        for (int i = 0; i < 20; i++) { //200 hundred times will be called
            executor.submit(new Runnable() {
                public void run() {
                    Connectionn.getInstance().connect();
                }
            });
        }

        executor.shutdown();
        executor.awaitTermination(1, TimeUnit.DAYS);
    }
}

public class Connectionn {

	private static Connectionn instance = new Connectionn();

	private Semaphore sem = new Semaphore(10, true);

	private Connectionn() {
	}

	public static Connectionn getInstance() {
		return instance;
	}

	public void connect() {
		try {
			// get permit decrease the sem value, if 0 wait for release
			sem.acquire();
			System.out.printf("%s:: Current connections (max 10 allowed): %d\n", 
					Thread.currentThread().getName(), sem.availablePermits());
			// do your job
			System.out.printf("%s:: WORKING...\n", Thread.currentThread().getName());
			Thread.sleep(2000);
		} catch (InterruptedException ignored) {
		} finally {
			// release permit, increase the sem value and activate waiting thread
			sem.release();
			System.out.printf("%s:: Connection released. Permits Left = %d\n", 
					Thread.currentThread().getName(), sem.availablePermits());
		}
	}
}
```
