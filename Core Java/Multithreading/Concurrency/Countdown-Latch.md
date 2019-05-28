## Countdown Latch
It is a class in java.util.concurrent package which allows one or more threads to wait until given set of operations is complete.
CountdownLatch has to be initialized with a count. Now if a thread calls await method on latch it has to wait until the latch count becomes 0. Other threads which are performing operations can decrement the count of latch by using countDown method.

Example -
```
CountDownLatch latch = new CountDownLatch(3);

Waiter      waiter      = new Waiter(latch);
Decrementer decrementer = new Decrementer(latch);

new Thread(waiter)     .start();
new Thread(decrementer).start();

Thread.sleep(4000);


public class Waiter implements Runnable{

    CountDownLatch latch = null;

    public Waiter(CountDownLatch latch) {
        this.latch = latch;
    }

    public void run() {
        try {
            latch.await();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Waiter Released");
    }
}

public class Decrementer implements Runnable {

    CountDownLatch latch = null;

    public Decrementer(CountDownLatch latch) {
        this.latch = latch;
    }

    public void run() {

        try {
            Thread.sleep(1000);
            this.latch.countDown();

            Thread.sleep(1000);
            this.latch.countDown();

            Thread.sleep(1000);
            this.latch.countDown();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
Since Waiter has invoked await method, it will wait until the latch count becomes 0.
