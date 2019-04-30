|Spring|EJB|
|---|---|
|Light weight|Heavy weight|
|Loosely copuled|Tightly coupled|
|Needs only jdk|EJB app server to run|

**Advantages of Spring**
* Makes your application light-weight as it ensures loose coupling.

**IOC container** 
* Can read XML file to identify all the dependencies of our classes.
* Create bean instances.
* It also manage life cycle of POJO classes.
* It performs Dependency Injection, also supply runtime parameters.
* IOC contains 2 containers **Core(BeanFactory)** & **J2EE(ApplicationContext)** & MVC contains 1 container i.e. **Web(WebApplicationContext)**
* BeanFactory has an implementation class i.e. XMLBeanFactory.
* ApplicationContext it has an implementation class ConfigurableApplicationContext, which is implemented by ClassPathXMLApplicationContext.
* We can start XMLBeanFactory/ClassPathXMLApplicationContext by using new XMLBeanFactory()/ClassPathXMLApplicationContext().
* For Standalone application, possible bean scopes are singleton & prototype.
* For Web Applications, possible bean scopes are singleton, prototype, request, session & context.
* The main root tag in the spring xml file is beans.

XML structure looks like -
```
<beans>
	<bean class="com.Text" id="t">
	</bean>
</beans>
```

* Servlet Container performs following, read web.xml & manage life cycle of our servlets. If you have some parameters 
you can supply them using init-param & context-param which are supplied to Servlet.

**Diff b/w BeanFactory & ApplicationContext**
* BeanFactory creates object when getBean() method is called i.e. on demand i.e. This is called Lazy Container.
* ApplicationContext creates object when container loads the spring XML files. This is called Eager Container(in case if bean scope is singleton). This has more features as compared to BeanFactory, that's why it is recommended.

* For scope prototype both containers create instances on user request.

* Containers create objects using Class.forName(). Spring can create instances even if the constructor is private for the class. It internally uses reflexion, it access the constructor of your class & then create instance.
* By using reflexion we can also create instance of classes with private constructor.

**Types of DI i.e. Setter & Constructor.**

* Setter DI - specifying property tag it passes the value to setter methods, this tag can have value attribute or it can also have value tag as child of property tag. You can only supply 1 parameter, this is the limitation of setter DI.
```
<bean>
	<property name="address" value="">
</bean>
```
* Constructor DI - here also you can have value attribute or value tag. 
	* if you don't specify constructor-arg it will call default constructor. 
	* If you have overloaded constructors then if 1st constructor has String arguement then 2nd constructor can't have String arguement & in this case while initializing you have to specify type attribute to decide which constructor to invoke.
	* You can specify multiple constructor-arg tags to call constructor with more than 1 args. You can specify index to specify which value to pass in which arguement.
```
<bean>
	<constructor-arg value="">
</bean>
```

* In case if you have User Defined Object to pass you should use "ref" attribute. This is pass by reference.
* In case if you want to pass by Object, we can use inner-bean tag in property/constructor-arg tag.
* If you want to pass array values then you can use "list" tag in between property/constructor-arg, this list tag can have multiple value tags or multiple ref tag.

**for passing collections**
* list - we have to use ***list*** tag in property/constructor-arg tag. It creates ArrayList object by default.
* set - we have to use ***set*** tag in property/constructor-arg tag. It creates LinkedHashSet object by default.
* map - we can have ***map*** tag which contains entry tag with key & value attribute. It creates LinkedHashMap object 
by default.
	
* If you want to create any specific collection you can use ***util:list***, ***util:map***, ***util:set*** tag where you can specify class name in property/constructor-arg tag.

* If you have a Properties object in your class, you can initialize it using <props> tag within <property> tag.

* If you want to load data from properties file then you can use ***property*** tag within which you can use ***util:properties*** & specify the file location.

* Constructor dependency injection is compulsory.

**dependency-check** attribute is used to specify whether setter DI is compulsory for your beans.
* possible values none, simple, objects & all
	* none means it is not necessary to pass any args to setter injections.
	* simple means it is compulsory to initialize all primitives
	* object means it is compulsory to initialize all objects
	* all means it is compulsory to initialize all parameters in bean

* dependency-check is equivalent to @Required annotation on setter methods. To use @Required, you need to instatiniate
***RequiredAnnotationBeanPostProcessor***.

* If class has a dependency of other class, we can use ***depends-on***, A depends-on B. depends-on is an attribute in  bean tag, you can specify reference of the bean in depends-on attribute.
	
**p & c namespace**, 
* **p namespace** is used for setter DI. 
Lest say Test class has properties name & car then we can set them using p namespace as below -
```
<bean id="car" class="beans.Car"/>
<bean id="t" class="beans.Test" p:name="Deepak" p:car-ref="car"/>
```
* **c namespace** is used for constructor DI.
Lest say Test class has properties name & car & it has a constructor with both attribute then we can set them using c namespace as below -
```
<bean id="car" class="beans.Car"/>
<bean id="t" class="beans.Test" c:name="Deepak" c:car-ref="car"/>
```

**Autowiring**
* Automatic dependency injection, can be used only for secondary data types. 
* Autowiring is of following types byType, byName, constructor, auto-detect & no. 
	* byType - it will look for beans of that type & inject it, if there are multiple beans of same type, it gives
	ambiguity. We can solve that ambiguity by using ***autowire-candidate*** as false on all beans except 1.
	* byName - it checks for the beans with type & name(name of property in dependent class) & then inject it.
	* constructor - if you have constructor DI in your class. It checks for constructor & when it finds 1, it will
	check parameters & then search those beans in application context byType.
	* auto-detect - if you don't know whether your class as constructor or setter DI. In this case if it finds 
	deafult constructor then it uses to initialize the bean & then call setters, otherwise it uses parameterized
	constructor & doesn't use setters.

* bean tag has autowire attribute for that particular bean.
* beans tag also has autowire attribute which applies to bean declared in it.
* @Autowired annotation can also be used, which is byType default. For this we don't need any constructor & setter in our class.
* @Qualifier annotation can be used to specify the name of bean to inject. So if you have multiple beans of same type then @Qualifier is required.
* To activate this you need to instatiniate AutowiredAnnotationBeanPostProcessor class. 

**Stereo types** - this will create bean instances
* @Controller
* @Service
* @Repository
* @Component
* to use this we need to add a tag, which scans all the classes in base-package.
```
<context:component-scan base-package=""/>
``` 

* context-annotation-config, activates all the annotation i.e @Required, @Autowired & all stereo types, if we 
	use this then we don't need to instatiniate any AutowiredAnnotationBeanPostProcessor. So just specify 
	context:component-scan & context:annotation-config it will take care of instatinating & autiwiring all objects.
```
<context:annotation-config/>
```

* Automatic Dependency Injection works only for secondary parameters or objects in classes.
* You can instantiate classes with static variables, for ex -
```
package beans;
class Car {
	private static String name;
	
	public static setName(String name){
		Car.name = name;
	}
}
```
we can use **MethodInvokingFactoryBean** as below -
```
<bean class="org.springframework.beans.factory.config.MethodInvokingFactoryBean">
	<property name="staticMethod" value="beans.Car.setName"/>
	<property name="arguements">
		<list>
			<value>Audi</value>
		</list>
	</property>
</bean>
```

* bean provides factory-method attribute which can be used to invoke factory-method of the class to get the instances.
```
Calendar calendar = Calendar.getInstance() //Factory class returning same class instance.
<bean id="c" class="java.util.Calendar" factory-method="getInstance"/>


LoggerFactory.getLogger(); //returns Logger class object.
<bean id="l" class="java.util.Logger" factory-method="getLogger"/>
```
* if your bean objects are created from instance methods instead of static methods, then too you can use,  factory-method along with factory-bean.
* Ex:you have SessionFactory object, using which you will call getSession to get Session object.
```
<bean id="sf" class="[actual-package].SessionFactory"/>
<bean id="sf" factory-bean="sf" factory-method="openSession" />
```
