## Cyclic Barrier
Its kind of checkpoint where we want all the threads to reach first & then proceed. So if we have 2 such cyclic barriers it would look like below. So basically we want all out threads to stop at barrier 1 until all threads reach there & then proceed & then wait at barrier 2 until all thread reach there & then proceed.

![Cyclic Barrier](https://github.com/deepakmotlani/Notes/blob/master/Core%20Java/Multithreading/images/cyclic-barrier.png)

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
