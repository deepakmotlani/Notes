## Junit Testing

**spring-boot-starter-test** constains following libraries -
* Junit 4
* Spring Test
* AssertJ
* Hamcrest
* Mockito
* JSONassert
* JsonPath

### Testing with Junit & Mockito

* @Runwith - provided by Junit, attaches runner with test class to initialize test data
* @Test - provided by Junit, use to indicate a test case
* @InjectMock - provided by Mockito, used to create & inject mock object
* @Mock - provided by Mockito, used to create the object to be injected

### Mockito add behaviour
```
Mockito.when(calcService.add(10, 20)).thenReturn(30); 
```
Here we have instrcuted Mockito that when add method is called on calcService with parameters 10 & 20 then return 30.

```
Mockito.when(calcService.add(10, 20)).thenCallRealMethod(); 
```
Here we have instrcuted Mockito that when add method is called on calcService with parameters 10 & 20 
then call real method.

### Mockito verify behaviour
```
Mockito.verify(calcService).add(10, 20);
```
Using this we verify that add method of calcService was called with parameters 10 & 20. It fails the test case if,
add method is not called or is called with different arguements.

Mockito also provides a check on the number of calls to method
```
Mockito.verify(calcService, Mockito.times(1)).add(10, 20);
```

Mockito also provides a check if a method was never called
```
Mockito.verify(calcService, Mockito.never()).subtract(10, 20);
```

Mockito also provides additional methods to verify
* atLeast(int min)
* atLeastOnce()
* atMost(int max)

### Mockito exception handling
```
@Test(expected = RuntimeException.class)
public void testAdd(){
	Mockito.doThrow(new RuntimeException('This is in calcService')).when(calcService).add(10, 20);
}
```
Using doThrow we can have mocks to throw exception when add method is called on calcService.
We can also specify expected attribute in @Test annotation, which means we expect this test case to throw exception.


### Mockito ordered verification
Mockito provides InOrder class using which we can verify the order in which methods are called on mocks.
```
public void testOrder() {
	calcService.add(10, 20);
	calcService.subtract(30, 20);
	
	InOrder order = Mockito.inOrder(calcService);
	
	order.verify(calcService).add(10, 20);
	order.verify(calcService).subtract(30, 20);
}
```

### Mockito spying
Mockito provides option to call real method on real object.
```
@Spy
private CalcService calcService;

public void addTest() {
	calcService.add(10, 20);
}
```

### Difference b/w Mock & Spy
When you mock a service & if a method of that service is called, then it returns null, if you don't specify the
behaviour for method. While in case of Spy the since actual method is called, you don't have to specify the 
behaviour(i.e. thenReturn).

### Mockito Reset
Mockito provides a reset capability so that it can be reused.
```
@Mock
private CalcService calcService;

public void testAdd() {
	calcService.add(10, 20);
	
	Mockito.reset(calcService);
}
```

### Junit provides following annotations
* @BeforeClass – Run once before any of the test methods in the class, public static void
* @AfterClass – Run once after all the tests in the class have been run, public static void
* @Before – Run before @Test, public void
* @After – Run after @Test, public void
* @Test – This is the test method to run, public void