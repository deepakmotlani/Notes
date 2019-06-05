## Mock static methods

With mockito we can't mock static methods of class. For testing static methods we can make use of power-mockito.
Power mockito works along with Mockito to test static methods.

**Adding following dependencies for power-mockito**

```
<dependency>
  <groupId>org.powermock</groupId>
  <artifactId>powermock-api-mockito</artifactId>
  <version>1.6.4</version>	  
</dependency>
<dependency>
	<groupId>org.powermock</groupId>
	<artifactId>powermock-module-junit4</artifactId>
	<version>1.6.4</version>
	<scope>test</scope>
</dependency>
```

```
public class WorkflowService {	
	public static String getCar(String carName, int price) {
		return "Jaguar";
	}
	
	public final String getString() {
		return "Hello World";
	}
}

@RunWith(PowerMockRunner.class)
@PrepareForTest(value = WorkflowService.class)
public class WorkflowServiceTest {
		
	@Test
	public void constructor() throws Exception {
		WorkflowService mock = PowerMockito.mock(WorkflowService.class);

		PowerMockito.whenNew(WorkflowService.class).withNoArguments().thenReturn(mock);
				
		new WorkflowService();
		PowerMockito.verifyNew(WorkflowService.class).withNoArguments();
	}
	
	@Test
	public void final_getString() throws Exception {
		WorkflowService mock = PowerMockito.mock(WorkflowService.class);
		PowerMockito.when(mock.getString()).thenReturn("Hi Deepak");
		
		String result = mock.getString();
		Assert.assertEquals(result, "Hi Deepak");	
	}
	
	@Test
	public void test_getCar_UsingMatchers() {
		PowerMockito.mockStatic(WorkflowService.class);
		PowerMockito.when(WorkflowService.getCar("Audi", 1000)).thenReturn("Deepak");	
		
		String result = WorkflowService.getCar("Audi", 1000);
		
		PowerMockito.verifyStatic(Mockito.atLeastOnce());
		Assert.assertEquals(result, "Deepak");		
	}
}


```

**So here we have used following things**
* @RunWith, now uses PowerMockRunner class
* @PrepareForTest, comes with power-mockito where we can specify class with static methods
* PowerMockito.mockStatic(Class class), used to mock class with static methods
* PowerMockito.when(), PowerMockito.whenNew(), for adding behaviour
* PowerMockito.verifyStatic(Mockito.atLeastOnce()), used to verify static method was once called