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