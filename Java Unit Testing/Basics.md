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