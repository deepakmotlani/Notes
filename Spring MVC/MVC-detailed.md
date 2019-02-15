**<mvc:annotation-drivern>** is used for enabling Spring MVC components with its default configurations. If you don't include this, then too your MVC application will work with **context:component-scan** for creating beans.
But mvc:annotation-driven does some extra job on configuring some special beans like HandlerMapping & HandlerAdapter.
In addition it also applies some defaults like, support for formatting number fields with @NumberFormat, support for reading & writing JSON, if jackson is on classpath.

**context:annotation-config**, resolves @Autowired & @Qualifier annotations for the beans which are already created & stored in spring container. on the contrary **context:component-scan** also scans the package for registering the beans & also wire the beans.
