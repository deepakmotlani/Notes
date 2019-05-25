## Adding a Controller

You can create a RestController by using below code i.e. RestController & RequestMapping are annotations provided by
Spring MVC

```
@RestController
public class HelloController {

	@RequestMapping(value = "/hello")
	public String sayHello() {
		return "Hello";
	}
}

```

Spring Boot has embedded tomcat on which our code runs.

## Adding customized behaviour
Using properties files on classpath, you can customize the behaviours. In order to do so we need to know the appropriate keys.

For example, if I want to change the tomcat port, I can do so by specifying below in application.properties
```
server.port=8081
```

You can find all such properties here - 
[Spring Boot Application Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html)