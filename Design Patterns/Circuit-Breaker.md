## Circuit Breaker

So in modern applications we make calls to external application API's or make remote calls, now those calls may complete or break or become
unresponsive. So calling application may also become unresponsive because of those remote call's.

Circuit Breaker is a solution to this problem. Basic idea is we wrap the remote call in a circuit breaker object, which monitors for failures.
Once failures reach certain threshold value, circuit breaker trips & all the further calls to circuit breaker returns with error or some
alternative message, without even calling the remote api. This will make sure that system become responsive & doesn't wait for unresponsive
calls.

**Different States of the Circuit Breaker**
The circuit breaker has three distinct states: Closed, Open, and Half-Open:
* **Closed** – When everything is normal, the circuit breaker remains in the closed state and all calls pass through to the services. When the 
number of failures exceeds a predetermined threshold the breaker trips, and it goes into the Open state.
* **Open** – The circuit breaker returns an error for calls without executing the function.
* **Half-Open** – After a timeout period, the circuit switches to a half-open state to test if the underlying problem still exists. 
If a single call fails in this half-open state, the breaker is once again tripped. If it succeeds, the circuit breaker resets back to the 
normal, closed state. 

**Netflix’s Hystrix** library provides an implementation of the Circuit Breaker pattern. Spring Cloud Netflix Hystrix looks for any 
method annotated with the @HystrixCommand annotation, and wraps that method in a proxy connected to a circuit breaker so that 
Hystrix can monitor it.

```
@EnableCircuitBreaker
@RestController
@SpringBootApplication
public class ReadingApplication {

  @Autowired
  private BookService bookService;

  @Bean
  public RestTemplate rest(RestTemplateBuilder builder) {
    return builder.build();
  }

  @RequestMapping("/to-read")
  public String toRead() {
    return bookService.readingList();
  }

  public static void main(String[] args) {
    SpringApplication.run(ReadingApplication.class, args);
  }
}

@Service
public class BookService {

  private final RestTemplate restTemplate;

  public BookService(RestTemplate rest) {
    this.restTemplate = rest;
  }

  @HystrixCommand(fallbackMethod = "reliable")
  public String readingList() {
    URI uri = URI.create("http://localhost:8090/recommended");

    return this.restTemplate.getForObject(uri, String.class);
  }

  public String reliable() {
    return "Cloud Native Java (O'Reilly)";
  }
}
```

You’ll also notice that we’ve added one last annotation, @EnableCircuitBreaker; that’s necessary to tell Spring Cloud that the 
Reading application uses circuit breakers and to enable their monitoring, opening, and closing.
