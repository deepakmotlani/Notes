- **@Component** annotation is added to the class, so that when Spring framework will scan for the components, this class will be treated as component. @Component annotation can be applied only to the class and it’s retention policy is Runtime.
- **@Autowired** annotation is used to let Spring know that autowiring is required. This can be applied to field, constructor and methods. This annotation allows us to implement constructor-based, field-based or method-based dependency injection in our components.
- **@Configuration** annotation is used to let Spring know that it’s a Configuration class.
- **@ComponentScan** annotation is used with @Configuration annotation to specify the packages to look for Component classes.
- **@Bean** annotation is used to let Spring framework know that this method should be used to get the bean implementation to inject in Component classes.

**AnnotationConfigApplicationContext** is the implementation of AbstractApplicationContext abstract class and it’s used for autowiring the services to components when annotations are used.

**ClassPathXmlApplicationContext** is used to get the ApplicationContext object by providing the configuration files location. It has multiple overloaded constructors and we can provide multiple config files also.

Both of these classes are part of **spring-context** dependency.
