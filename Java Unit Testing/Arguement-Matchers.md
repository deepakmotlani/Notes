## Arguement Matchers

When adding behaviour we have to specify parameters of method like below
```
Mockito.when(calcService.add(10, 20)).thenReturn(30);
```

But we may want to work for broader range of parameters, that can be done by Arguement Matchers, like below
```
Mockito.when(calcService.add(Matchers.anyInt(), Matchers.anyInt())).thenReturn(30);
```
Using this we specify that for any integer parameters, we want to return 30.

**Matchers is provided by org.mockito package.**
* Can't be used in return arguements.
* Can't be used outside of verification or stubbing.
* When used, have to be used for all arguements. 

Incorrect example
```
String orMatcher = Matchers.or(Matchers.eq("poppy"), Matchers.endsWith("y"));
Mockito.verify(mock).analyze(orMatcher);
```

Correct example
```
Mockito.verify(mock).analyze(Matchers.or(Matchers.eq("poppy"), Matchers.endsWith("y")));
```

**Mockito provides additional matchers to implement common logical operations (not, and, or).**

**Matchers provides many more methods**
* Matchers.any(Class class), can be used for custom classes
* Matchers.anyDouble(), Matchers.anyFloat() etc. for all the wrapper clasess


## Arguement Captors

This is a recommended way of matching arguements because it makes tests clean & simple.

```
public class TestClass {

	@Captor
	private ArgumentCaptor<Integer> integerArgumentCaptor;
	
	@Captor
	private ArgumentCaptor<String> stringArgumentCaptor;

	@Test
	public void test_getCar() {
		Mockito.when(workflowService.getCar(Matchers.anyString(), Matchers.eq(1000))).thenReturn("Maruti");
		
		String result = workflowController.getName(); //internally calls workflowService.getCar("Audi", 1000)
		
		Mockito.verify(workflowService).getCar(stringArgumentCaptor.capture(), integerArgumentCaptor.capture());
		Assert.assertEquals(result, "Maruti");		
		Assert.assertEquals((Integer)integerArgumentCaptor.getValue(), (Integer)1000);
		Assert.assertEquals((String)stringArgumentCaptor.getValue(), "Audi");
	}
}
```
