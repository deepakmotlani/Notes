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
