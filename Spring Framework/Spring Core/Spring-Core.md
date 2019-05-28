- **@Component** annotation is added to the class, so that when Spring framework will scan for the components, this class will be treated as component. @Component annotation can be applied only to the class and it’s retention policy is Runtime. This is genric stereo-type for any Spring Managed Component.
 - **@Repository** stereotype for persistence layer.
 - **@Service** stereotype for service layer.
 - **@Controller** stereotype for presentation layer (spring-mvc).
- **@Autowired** annotation is used to let Spring know that autowiring is required. This can be applied to field, constructor and methods. This annotation allows us to implement constructor-based, field-based or method-based dependency injection in our components. It accepts optional boolean parameter "required", with default value as true. If set to false, the dependency becomes optional.
- **@Resource** This annotation takes an optional name argument. In case no name attribute is specified with this annotation, the default name is interpreted from the field-name or the setter method (i.e. the bean property name). Always remember that if the @Resource annotation doesn’t find the bean with the name it will automatically switch it’s autowiring technique to autowire=byType (i.e. @Autowired annotation).
- **@Configuration** annotation is used to let Spring know that it’s a Configuration class.
- **@ComponentScan** annotation is used with @Configuration annotation to specify the packages to look for Component classes.
Or if we write <context:component-scan base-package=""/> it is similar, it will scan all the classes in base-package which are annotated with @Component, @Repository, @Service, @Controller. This also resolves @Autowired & @Qualifier annotations.
- **@Bean** annotation is used to let Spring framework know that this method should be used to get the bean implementation to inject in Component classes.

- **@Qualifier** is useful for the situation where you have more than one bean matching the type of dependency and thus resulting in ambiguity.

**AnnotationConfigApplicationContext** is the implementation of AbstractApplicationContext abstract class and it’s used for autowiring the services to components when annotations are used.

**ClassPathXmlApplicationContext** is used to get the ApplicationContext object by providing the configuration files location. It has multiple overloaded constructors and we can provide multiple config files also.

Both of these classes are part of **spring-context** dependency.
