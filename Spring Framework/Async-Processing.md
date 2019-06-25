## Asynchronous processing in Spring applications

**@EnableAsync** - used to enable async support. This should be used with @Configuration annotation.

```
@Configuration
@EnableAsync
public class SpringAsyncConfig { 

}
```

**@Async** - This annotation is used with method which you want to run asynchronously.

Methods with void return type -
```
@Async
public void asyncMethodWithVoidReturnType() {
    System.out.println("Execute method asynchronously. "
      + Thread.currentThread().getName());
}
```

Methods with return type - returns Future object
```
@Async
public Future<String> asyncMethodWithReturnType() {
    System.out.println("Execute method asynchronously - "
      + Thread.currentThread().getName());
        
	return new AsyncResult<String>("hello world !!!!");    
}
```

**Executor** - By default Spring uses SimpleAsyncTaskExecutor to run methods asynchronously. But we can override this
default behaviour at method level or at application level.

**Method level** - 
```
@Configuration
@EnableAsync
public class SpringAsyncConfig {
     
    @Bean(name = "threadPoolTaskExecutor")
    public Executor threadPoolTaskExecutor() {
        return new ThreadPoolTaskExecutor();
    }
}

@Async("threadPoolTaskExecutor")
public void asyncMethodWithConfiguredExecutor() {
    System.out.println("Execute method with configured executor - "
      + Thread.currentThread().getName());
}
```

**Application level** -
```
@Configuration
@EnableAsync
public class SpringAsyncConfig implements AsyncConfigurer {
     
    @Override
    public Executor getAsyncExecutor() {
        return new ThreadPoolTaskExecutor();
    }
     
}
```