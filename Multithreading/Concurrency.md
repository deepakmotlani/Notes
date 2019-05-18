## Concurrenct Package

**Executor Service**
ExecutorService is a construct that allows you to pass your task to be executed by a thread asynchronously. It 
creates & maintains a pool of threads for executing submitted tasks. It also manages a queue internally for 
awaiting tasks until the thread becomes available. You can instantiate ExecutorService by 2 methods,
1. Manually by passing individual parameters i.e. corePoolSize, maxPoolSize, keepAliveTime, workerQueue etc.
2. Executors static factory methods i.e. Executors.newFixedThreadPool(10) or Executors.getNewSingleThreadExecutor()

ExecutorService also provides shutdown() method, when called it will allow previously submitted tasks to be executed
before terminating, while shutdownnow(), will prevent waiting tasks to start & currently excuting task to stop.

2 commonly used methods in ExecutorService are 
* void execute(Runnable) // this is inherited from interface Executor
* Future<V> submit(Callable<V>)

|Callable<V>|Runnable|
|---|---|
| Part of the java.util.concurrent package since Java 1.5|Part of the java.lang package since Java 1.0|
|It is a parameterized interface, such as Callable<V>|It is a non-parameterized interface|
|Can throw a checked Exception|Cannot throw a checked Exception|
|Contains a single method, called call (), which has return Type V, the same as of the defined interface parameter Type|Contains a single method, called run (), which returns void|

**What is Future**
Future interface is a generic interface, which represents value returned by asynchronous operations. It contains
method to check wether the callable has finished its execution & then only it fetches the value otherwise waits.
The get() method of Future blocks calling thread & waits until Callable completes its execution. This interface 
also contains methods to cancel Callable's execution. However once the Callable computation is complete, it can't
be cancelled.

**Runnable Example with Executor Service**
```
public class RunnableFactorialExecutorService {
	public class Factorial implements Runnable {
		private int number;
		
		public Factorial(int num) {
			number = num;
		}
		
		@Override
		public void run() {
			int fact = number;
			for(int i = number - 1; i > 1; i--) {
				fact *= i;
			}
			System.out.println(fact);
		}
	}
	
	public static void main(String[] args) {
		RunnableFactorialExecutorService runnableFactorial = new RunnableFactorialExecutorService();
		ExecutorService executorService = Executors.newSingleThreadExecutor();
		Factorial factorial = runnableFactorial.new Factorial(10);
		executorService.execute(factorial);
		executorService.shutdown();
	}
}

```

**Callable Factorial with Executor Service**
```
public class CallableFactorial {
	public class Factorial implements Callable<Integer> {
		private int number;
		
		public Factorial(int num) {
			number = num;
		}
		
		@Override
		public Integer call() throws InterruptedException{
			int fact = number;
			for(int i = number - 1; i > 1; i--) {
				fact *= i;
			}
			Thread.sleep(10);
			return fact;
		}
	}
	
	public static void main(String[] args) throws InterruptedException, ExecutionException {
		CallableFactorial callableFactorial = new CallableFactorial();
		ExecutorService executorService = Executors.newSingleThreadExecutor();
		Factorial factorial = callableFactorial.new Factorial(10);
		Future<Integer> future = executorService.submit(factorial);
		System.out.println(future.get());
		System.out.println("Hey I am done");
		executorService.shutdown();
	}
}

```

RunnableFuture provides an implementation i.e. FutureTask<V>, using which you can perform operations on result
```
public class CallableFactorial {
	public class Factorial implements Callable<Integer> {
		private int number;
		
		public Factorial(int num) {
			number = num;
		}
		
		@Override
		public Integer call() throws InterruptedException{
			int fact = number;
			for(int i = number - 1; i > 1; i--) {
				fact *= i;
			}
			Thread.sleep(10);
			return fact;
		}
	}
	
	public class Result extends FutureTask<Integer> {
		public Result(Callable<Integer> callable) {
			super(callable);		
		}
		
		@Override
		public void done() {
			if(this.isDone()) {
				try {
					System.out.println("Hey Factorial is calculated as " + this.get());
				} catch (InterruptedException | ExecutionException e) { 
					e.printStackTrace();
				}
			}
		}
		
	}
	
	public static void main(String[] args) throws InterruptedException, ExecutionException {
		CallableFactorial callableFactorial = new CallableFactorial();
		ExecutorService executorService = Executors.newSingleThreadExecutor();
		
		Factorial factorial = callableFactorial.new Factorial(10);
		Result result = callableFactorial.new Result(factorial);
		executorService.submit(result);		
		
		executorService.shutdown();
	}
}


```