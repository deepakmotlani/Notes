## Blocking Queue

java.util.concurrent provides BlockingQueue interface, which is used for producer  & consumer systems. Producer threads produce data
& put it in the blocking queue until a specified limit & after that it is blocked when it tries to insert more data & remains blocked until
Consumer thread doesn't consume data from queue. On the contrary Consumer thread keep consumiing data from queue until any data is available
post that consumer thread will be blocked until Producer produces some data.

It has methods which would throw exeptions or block the threads or return special value i.e. true or false.

|Throws Exception|Special Value|Blocks|Times Out|
|---|---|---|---|
|Insert|add(o)|offer(o)|put(o)|offer(o, timeout, timeunit)|
|Remove|remove(o)|poll()|take()|poll(timeout, timeunit)|
|Examine|element()|peek()|

Various implementations of BlockingQueue are ArrayBlockingQueue, SynchronousQueue etc.

Example
```
public class BlockingQueueExample {

    public static void main(String[] args) throws Exception {

        BlockingQueue queue = new ArrayBlockingQueue(1024);

        Producer producer = new Producer(queue);
        Consumer consumer = new Consumer(queue);

        new Thread(producer).start();
        new Thread(consumer).start();

        Thread.sleep(4000);
    }
}

public class Producer implements Runnable{

    protected BlockingQueue queue = null;

    public Producer(BlockingQueue queue) {
        this.queue = queue;
    }

    public void run() {
        try {
            queue.put("1");
            Thread.sleep(1000);
            queue.put("2");
            Thread.sleep(1000);
            queue.put("3");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class Consumer implements Runnable{

    protected BlockingQueue queue = null;

    public Consumer(BlockingQueue queue) {
        this.queue = queue;
    }

    public void run() {
        try {
            System.out.println(queue.take());
            System.out.println(queue.take());
            System.out.println(queue.take());
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

## Concurrent Map
This is an interface in java.util.concurrent package which is capable of handling concurrent access i.e. puts & gets on it. One of the implementation is ConcurrentHashMap which offers better concurreny than HashTable. ConcurrentHashMap doesn't lock the map when you are
reading it, ConcurrentHashMap doesn't lock the entire map while you are writing to it, it internally locks only parts of map.

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

## Cyclic Barrier
Its kind of checkpoint where we want all the threads to reach first & then proceed. So if we have 2 such cyclic barriers it would look like below. So basically we want all out threads to stop at barrier 1 until all threads reach there & then proceed & then wait at barrier 2 until all thread reach there & then proceed.

![Cyclic Barrier](https://github.com/deepakmotlani/Notes/blob/master/Multithreading/images/cyclic-barrier.png)

```
/*Creating cyclic barrier, specifying that 2 threads will wait at barrier.*/
CyclicBarrier barrier = new CyclicBarrier(2); 

/*Threads wait at barrier by calling await() method, once n threads have reached barrier, all threads are released for execution*/
barrier.await();
OR
barrier.await(10, TimeUnit.SECONDS); //wait for certain time period

public static void main(String args[]) {
    Runnable barrier1Action = new Runnable() {
        public void run() {
            System.out.println("BarrierAction 1 executed ");
        }
    };
    Runnable barrier2Action = new Runnable() {
        public void run() {
            System.out.println("BarrierAction 2 executed ");
        }
    };

    CyclicBarrier barrier1 = new CyclicBarrier(2, barrier1Action); //barrier1Action is executed when 2 threads reach the barrier
    CyclicBarrier barrier2 = new CyclicBarrier(2, barrier2Action); //barrier2Action is executed when 2 threads reach the barrier

    CyclicBarrierRunnable barrierRunnable1 = new CyclicBarrierRunnable(barrier1, barrier2);
    CyclicBarrierRunnable barrierRunnable2 = new CyclicBarrierRunnable(barrier1, barrier2);

    new Thread(barrierRunnable1).start();
    new Thread(barrierRunnable2).start();
}

public class CyclicBarrierRunnable implements Runnable{
    CyclicBarrier barrier1 = null;
    CyclicBarrier barrier2 = null;

    public CyclicBarrierRunnable(CyclicBarrier barrier1, CyclicBarrier barrier2) {
        this.barrier1 = barrier1;
        this.barrier2 = barrier2;
    }

    public void run() {
        try {
            Thread.sleep(1000);
            System.out.println(Thread.currentThread().getName() + " waiting at barrier 1");
            this.barrier1.await();

            Thread.sleep(1000);
            System.out.println(Thread.currentThread().getName() + " waiting at barrier 2");
            this.barrier2.await();

            System.out.println(Thread.currentThread().getName() + " done!");
        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (BrokenBarrierException e) {
            e.printStackTrace();
        }
    }
}
```

Output
```
Thread-0 waiting at barrier 1
Thread-1 waiting at barrier 1
BarrierAction 1 executed
Thread-1 waiting at barrier 2
Thread-0 waiting at barrier 2
BarrierAction 2 executed
Thread-0 done!
Thread-1 done!
```
