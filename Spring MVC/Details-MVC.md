## Spring MVC provides -
1. Form based support
2. Multi Action Controller Support
3. Validation Support
4. Internationalization Support
5. Interceptors
6. View Resolvers
7. Exception Handling Support

* Spring MVC provides support from Presentation to Controller layer only. All the other layers i.e. Service & DAO, 
we have to use IOC itself.

* As per JSP modal architecture, we need to write common operations in Front Controller. If your front controller is
1. JSP then it is JSP Modal - 1.
2. Servlet then it is JSP Modal - 2.
3. Filter then it is JSP Modal - 3.
4. Tag Support then it is JSP Modal - 4.

Spring MVC is JSP modal - 2 architecture. So front controller should be a servlet. So all the common operations,
they provided in front controller servlet.

This is how we declare front controllers -
```
web.xml
<web-app>
	<servlet>
		<servlet-name>ds</servlet-name>
		<servlet-class>DisptacherServlet</servlet-class>
	</servlet>
	<servlet-mapping>
		<servlet-name>ds</servlet-name>
		<url-pattern>/registration</url-pattern>
		<url-pattern>/login</url-pattern> // or you can say /* to map all requests
	</servlet-mapping>
</web-app>
```
* Possible url-pattern
1. complete-path
2. /*, all requests
3. /*.ext, requests with ext will map, 
	ex: Struts has /*.do, /*.action & for spring we can use any extenstions like /*.htm etc

* Write Controller, using programmatic way, we need to extend eiter of these
1. Controller interface
2. AbstractController
3. AbstractCommandController
4. SimpleFormController
5. AbstractWizardFormController
6. MultiActionController

or you can use annotation way & use annotation @Controller on your class

If you create controller implementing Controller interface, you must override method handleRequest -
```
public ModelAndView handleRequest(HttpRequest request, HttpResponse response) throws Exception {
	Map map = new HashMap();
	map.put('message', "Hello");
	
	return new ModelAndView("successpage", map);
}

dispatcher-servlet.xml //using url-pattern it identifies servlet name
<beans>
	<bean name="/hello.htm" class="HelloController"> // this will forward hello.htm request to HelloController
	<bean class="InternalViewResolver"> // using this configuration, dispatcher-servlet will find successpage.jsp in output folder
		<property name="prefix" value="/output">
		<property name="suffix" value=".jsp">
	</bean>	
</beans>

```
Spring MVC lifecycle -
1. Request comes to DisptacherServlet, DisptacherServlet then calls HandlerMapping to identify which controller is
	to be called. 
2. Now DispatcherServlet creates Controller object & calls the controller method & passes the request & response object.
3. Now Controller response back to DispatcherServlet with modal & view. 
4. DispatcherServlet then calls InternalViewResolver to resolve the view.
5. InternalViewResolver reads configuration i.e. prefix & suffix from configuration & forms the actual location,
	where it has to find .jsp.
