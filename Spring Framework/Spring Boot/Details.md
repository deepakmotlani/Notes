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

## Connecting to database

Adding spring-boot-starter-data-jpa dependency on your pom.xml will add dependencies for JPA.
We can also use embedded database example - Apache Derby which will be added to our classpath by adding its 
dependency.

Good thing is that you don't even need to set the database connection properties when you work with embedded database.
It is all handled internally.

Now you can annotate your entities with @Entity annotation which tells JPA that this is going to be mapped with a
table in RDBMS & actually it will create Entity table as soon as we start our application.

Using @Id on one of the column signifies your primary key.

If you want to perform simple CRUD operations on any entity, you can simply create a Repository inerteface & extend
it from CrudRepository & this should provide implementations for all the common CRUD operations.

```
public interface TopicRepository implements CrudRepository<Topic, String> {
	/* 
		CrudRepository is a genric interface which accepts entity & its primary key type & this provides 
		implementations for all common CRUD operations.
		
		Iterable<Topic> findAll();
		save(Topic); works for both add & update, it internally identifies that it is a new object or old objec
		findOne(String); where String is primary key
		delete(String); where String is primary key
	*/
}
```

@ManyToOne annotation is used to show a relationship i.e.
Ex - every Course is for a particular Topic & likewise there could be many courses for a particular Topic, so when we
create entities, so this is like a foreign key
```
public class Course {
	// other fields
	
	@ManyToOne
	private Topic topic;
}
```
All the annotations i.e. @Entity, @Id, @Column, @ManyToOne etc. belong to javax.persistence package i.e. JPA, it has
nothing to do with Spring Boot or any ORM, but ORM frameworks understand these annotations.

Spring Data JPA also provides method for filters, for example -
```
@Entity
public class Course {

	@Id
	private String id;
	private String name;
	private Topic topic;
}

@Entity
public class Topic {
	private String id;
}

public interface CourseRepository extends CrudRepository<Course, String> {
	// this interface provides common methods as explained above, but it also provides implementations for
	// methods, if you provide proper name to methods i.e.
	
	public Iterable<Course> findByName(String name); // you don't have to provide implementation to this method,
	// Data JPA does it for you.
	
	public Iterable<Course> findByTopicId(String id); // so using this it Data JPA understands that it has to serach
	// through Topic's primary key i.e. Id, which is actually a foreign key for Course.
}
```
