## Semaphore

Semaphore is a kind of counting lock, which has 2 methods release() & acquire(). Semaphore is initialized with number of permissions or locks that can be acquired. Call to acquire() method is acquiring a lock & call to release() method is releasing the lock.

If no more permits/locks are available thread calling acquire() method will be blocked. Similarly call to release() method will be blocked if no more permits can be released to semaphore.

No guarantee about fairness of threads waiting to acquire permits from semaphore. That is there is no gaurantee that method calling the acquire method first will get the permit first.

To enforce fairness there is another constructor which takes boolean value to enforce fairness.
