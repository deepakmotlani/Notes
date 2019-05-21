## Thread Safety

Java supports multithreading, although multithreading is powerfool but it comes with cost/price. We need to write
implementations in thread-safe way. 

What does thread-safe mean?
This means multiple threads can access the same resource without giving any errors or unwanted output.

**Following Approaches** -

1. **Stateless Implementations** - In this example factorial method will always return the same result, no matter how
	many threads are running in parallel. This is called stateless implementation i.e. neither rely on external state
	nor maintain state at all.
```
public class MathUtils {
     
    public static BigInteger factorial(int number) {
        BigInteger f = new BigInteger("1");
        for (int i = 2; i <= number; i++) {
            f = f.multiply(BigInteger.valueOf(i));
        }
        return f;
    }
}
```

2. **Immutable Implementation** - If we want to share state b/w multiple threads, we can do so by making them 
	immutable. Class is immutable if its state can't be modified after creation. MessageService is immutable,
	in this example.
```
public class MessageService {
     
    private final String message;
 
    public MessageService(String message) {
        this.message = message;
    }
     
    // standard getter
     
}
```

3. **Thread-Local fields** - We can create multiple threads that don't share state with other threads. 

```
public class ThreadA extends Thread {
     
    private final List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
     
    @Override
    public void run() {
        numbers.forEach(System.out::println);
    }
}
public class ThreadB extends Thread {
     
    private final List<String> letters = Arrays.asList("a", "b");
     
    @Override
    public void run() {
        letters.forEach(System.out::println);
    }
}
```
Similar thing can be acheived by using ThreadLocal 
```
public class StateHolder {
     
    private final String state;
 
    // standard constructors / getter
}
public class ThreadState {
     
    public static final ThreadLocal<StateHolder> statePerThread = new ThreadLocal<StateHolder>() {
         
        @Override
        protected StateHolder initialValue() {
            return new StateHolder("active");  
        }
    };
 
    public static StateHolder getState() {
        return statePerThread.get();
    }
}
```

4. **Synchronized Collections** - We can create synchronized collections easily by using Collections class as below.
This uses intrinsic locks & has performance overhead, because only 1 thread can add values to collection at a time.
```
Collection<Integer> syncCollection = Collections.synchronizedCollection(new ArrayList<>());
Thread thread1 = new Thread(() -> syncCollection.addAll(Arrays.asList(1, 2, 3, 4, 5, 6)));
Thread thread2 = new Thread(() -> syncCollection.addAll(Arrays.asList(7, 8, 9, 10, 11, 12)));
thread1.start();
thread2.start();
```

5. **Concurrent Collections** - This are provided by java in java.util.concurrent package, which contains several
	collections like ConcurrentHashMap. Unlike synchronized collections, concurrent collections acheive thread
	safety by dividing their data into segments. In Concurrent Hashmap, multiple threads can acquire locks on
	different map segments, so multiple threads can access Map at same time.
```
Map<String,String> concurrentMap = new ConcurrentHashMap<>();
concurrentMap.put("1", "one");
concurrentMap.put("2", "two");
concurrentMap.put("3", "three");
```

6. **Atomic Objects** - is another of acheiving thread safety, using Atomic classes provided by Java i.e.
	AtomicInteger, AtomicLong, AtomicBoolean & AtomicReference in java.util.concurrent.atomic package. 
	Atomic classes allow us to perform multithreading operations, which are thread safe, without using synchronization.
```
public class Counter {
     
    private int counter = 0;
     
    public void incrementCounter() {
        counter += 1;
    }
     
    public int getCounter() {
        return counter;
    }
}
```
If we 2 thread execute this code simultaneously, in theory the value of counter will be 2, but we can't be sure of
result. But if we can make integer atomic as below
```
public class AtomicCounter {
     
    private final AtomicInteger counter = new AtomicInteger();
     
    public void incrementCounter() {
        counter.incrementAndGet();
    }
     
    public int getCounter() {
        return counter.get();
    }
}
```
Atomic operations works on CAS i.e. Compare & Swap, to ensure data integrity. Meaning if there is a memory location 
M, existing value at M is A, new value to be placed is B. CAS operation updates valus in M to B, only if existing
value matches A, otherwise no action is taken. When multiple threads want to update the value, one of them gets the
lock & is able to update the value while other is not able to update. However, in case of locks, no threads gets
suspended, 1 thread will update the value & then other thread will get lock to update the value. 
Another consequence in CAS approach is program logic becomes more complex, because developer has to handle both
scenarios i.e. succeed to update the value & failed to update the value, in which case it may repeat the operation
until it succeeds.
Main methods in Atomic classes are -
1. get() - gets the value from main memory, so changes from other threads are visible, equivalent to reading volatile
variable.
2. compareAndSet() - returns true if succeeds in updating else return false.
```
public class SafeCounterWithoutLock {
    private final AtomicInteger counter = new AtomicInteger(0);
     
    public int getValue() {
        return counter.get();
    }
    public void increment() {
        while(true) {
            int existingValue = getValue();
            int newValue = existingValue + 1;
            if(counter.compareAndSet(existingValue, newValue)) {
                return;
            }
        }
    }
}
```

7. **Synchronized Methods** - only 1 thread can enter any synchronized method for an object. They rely mainly on 
	intrinsic locks or monitor locks.
```
public synchronized void incrementCounter() {
    counter += 1;
}
```

8. **Synchronized Statements** - If we want to synchronize only specific parts of method, or we want to make calls
	to some methods which are not in our source code, we can do it using synchronized blocks.
```
public void incrementCounter() {
    // additional unsynced operations
    synchronized(this) {
        counter += 1; 
    }
}
```

9. **Volatile Fields** - Even if we used synchronization, class variables might be cached by CPU, so updates to those
	fields might not be visible to other threads. With volatile we instruct JVM & compiler to store the counter 
	variable in main memory & read from main memory, instead of CPU cache.

10. **Extrinsic Locks** - In this we use external entity to enforce excelusive access to resource. With intrinsic 
locking, where synchronized methods and blocks rely on the this reference, an attacker could cause a deadlock by 
acquiring the intrinsic lock and triggering a denial of service (DoS) condition. Unlike its intrinsic counterpart, 
an extrinsic lock makes use of a private entity, which is not accessible from the outside. 
This makes it harder for an attacker to acquire the lock and cause a deadlock.
```
public class ExtrinsicLockCounter {
 
    private int counter = 0;
    private final Object lock = new Object();
     
    public void incrementCounter() {
        synchronized(lock) {
            counter += 1;
        }
    }
     
    // standard getter
     
}
```

11. **Reentrant Locks** - With intrinsic locks, the lock acquisition model is rather rigid: one thread acquires the lock, 
then executes a method or code block, and finally releases the lock, so other threads can acquire it and access the 
method. There’s no underlying mechanism that checks the queued threads and gives priority access to the longest 
waiting threads. ReentrantLock instances allow us to do exactly that, hence preventing queued threads from 
suffering some types of resource starvation.
```
public class ReentrantLockCounter {
 
    private int counter;
    private final ReentrantLock reLock = new ReentrantLock(true);
     
    public void incrementCounter() {
        reLock.lock();
        try {
            counter += 1;
        } finally {
            reLock.unlock();
        }
    }
     
    // standard constructors / getter
     
}
```

12. **Read/Write Locks** - A ReadWriteLock lock actually uses a pair of associated locks, one for read-only operations 
and other for writing operations. As a result, it’s possible to have many threads reading a resource, 
as long as there’s no thread writing to it. Moreover, the thread writing to the resource will prevent other 
threads from reading it.
```
public class ReentrantReadWriteLockCounter {
     
    private int counter;
    private final ReentrantReadWriteLock rwLock = new ReentrantReadWriteLock();
    private final Lock readLock = rwLock.readLock();
    private final Lock writeLock = rwLock.writeLock();
     
    public void incrementCounter() {
        writeLock.lock();
        try {
            counter += 1;
        } finally {
            writeLock.unlock();
        }
    }
     
    public int getCounter() {
        readLock.lock();
        try {
            return counter;
        } finally {
            readLock.unlock();
        }
    }
 
   // standard constructors
    
}
```
