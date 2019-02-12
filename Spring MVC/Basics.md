![Spring MVC](https://github.com/deepakmotlani/Notes/blob/master/Spring%20MVC/images/MVC-basics.PNG)

## Following is the sequence of events corresponding to an incoming HTTP request to DispatcherServlet −

1. After receiving an HTTP request, DispatcherServlet consults the HandlerMapping to call the appropriate Controller.

1. The Controller takes the request and calls the appropriate service methods based on used GET or POST method. The service method will set model data based on defined business logic and returns view name to the DispatcherServlet.

1. The DispatcherServlet will take help from ViewResolver to pickup the defined view for the request.

1. Once view is finalized, The DispatcherServlet passes the model data to the view which is finally rendered on the browser.

All the above-mentioned components, i.e. HandlerMapping, Controller, and ViewResolver are part of WebApplicationContext which is an extension of the plainApplicationContext with some extra features necessary for web applications.
