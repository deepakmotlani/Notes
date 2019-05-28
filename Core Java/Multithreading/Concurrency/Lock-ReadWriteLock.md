## Lock

java.util.concurrent.Lock is a thread synchornization technique similar to synchronization mechanism, however it is more flexible & sophisticated.

First lock is created & then lock() method is called, any other thread calling lock() method will be blocked until thread call unlock() method & then unlock() method is called.
```
Lock lock = new ReentrantLock();

lock.lock();

//critical section

lock.unlock();
```

ReentrantLock is one of the implementation of Lock interface.

**The main differences between a Lock and a Synchronized block are:**

* A synchronized block makes no guarantees about the sequence in which threads waiting to entering it are granted access.
* You cannot pass any parameters to the entry of a synchronized block. Thus, having a timeout trying to get access to a synchronized block is not possible.
* The synchronized block must be fully contained within a single method. A Lock can have it's calls to lock() and unlock() in separate methods.

## ReadWriteLock

A java.util.concurrent.locks.ReadWriteLock is an advanced thread lock mechanism. It allows multiple threads to read a certain resource, but only one to write it, at a time. 

```
ReadWriteLock readWriteLock = new ReentrantReadWriteLock();

readWriteLock.readLock().lock();
    // multiple readers can enter this section
    // if not locked for writing, and not writers waiting
    // to lock for writing.
readWriteLock.readLock().unlock();

readWriteLock.writeLock().lock();
    // only one writer can enter this section,
    // and only if no threads are currently reading.
readWriteLock.writeLock().unlock();
```
