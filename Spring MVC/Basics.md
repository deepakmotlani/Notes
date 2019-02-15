![Spring MVC](https://github.com/deepakmotlani/Notes/blob/master/Spring%20MVC/images/MVC-basics.PNG)

## Following is the sequence of events corresponding to an incoming HTTP request to DispatcherServlet −

1. After receiving an HTTP request, DispatcherServlet consults the HandlerMapping to call the appropriate Controller.

1. The Controller takes the request and calls the appropriate service methods based on used GET or POST method. The service method will set model data based on defined business logic and returns view name to the DispatcherServlet.

1. The DispatcherServlet will take help from ViewResolver to pickup the defined view for the request.

1. Once view is finalized, The DispatcherServlet passes the model data to the view which is finally rendered on the browser.

All the above-mentioned components, i.e. HandlerMapping, Controller, and ViewResolver are part of WebApplicationContext which is an extension of the plainApplicationContext with some extra features necessary for web applications.

## web.xml
**context-param** is used to store some data for whole application.

**init-param** is used to store some data which is specific to a particular servlet.

## Application Context v/s Web Application Context

In Spring Web applications there are 2 types of containers, each of which is configured & initialized differently. One is **Application Context** & other is **Web Application Context**.

**Application Context** is container initialized by **ContextLoaderListener** or **ContextLoaderServlet** in web.xml, & this is how it is configured.

![Context Loader](https://github.com/deepakmotlani/Notes/blob/master/Spring%20MVC/images/web-xml-context-loader.PNG)

In the above configuration, I am asking spring to load all files that match -context.xml & create an Application Context from it. This context may contain-
1. Middle-tier transaction services
2. Data access objects & anything that you might want to use across application.

**Remember there is 1 Application Context per application.**

**Web Application Context** is the child context of application context. Each DispatcherServlet defined in Spring web application will have an associated web Application Context. This is how we initialize it.

![Dispatch Servlet](https://github.com/deepakmotlani/Notes/blob/master/Spring%20MVC/images/web-xml-dispatcher-servlet.PNG)

You should also specify the servlet-mapping tag to map the url-pattern which this servlet would handle. Specifying init-param in Dispatcher servlet is optional, if you don't specify it would take the contextConfigLocation as [servlet-name]-servlet.xml.

**Points to understand**
1. ContextLoaderListener creates a root web-application-context for web-application & puts it in ServletContext.
2. DispatcherServlet creates its own WebApplicationContext, handlers/controllers/view-resolvers are managed by this context.
3. When ContextLoaderListener is used in with DispatcherServlet, a root web-application-context is created first & a child-context is also created by DispatcherServlet & is attached to root-application-context.
