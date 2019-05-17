## Thread Safety

Java supports multithreading, although multithreading is powerfool but it comes with cost/price. We need to write
implementations in thread-safe way. 

What does thread-safe mean?
This means multiple threads can access the same resource without giving any errors or unwanted output.

Following Approaches -

1. Stateless Implementations - In this example factorial method will always return the same result, no matter how
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
