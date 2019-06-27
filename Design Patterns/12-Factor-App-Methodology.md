## Twelve Factor App Methodology

1. **Codebase** - One codebase tracked in version control & that can be used for many deployments. You should not 
create different repositories when you need different setup for production. You can have multiple branches, versions
to deploy on different environments.

2. **Dependencies** - All dependencies should be declared, with no implicit reliance on system tools or libraries.
As long as we are using standard build tools like npm, yarn, maven, gradle etc. we mostly have basics covered.


3. **Config** - Configuration that varies between deployments should be stored in the environment. It is very easy to
keep environment specific files in codebase & load them as per the environment in which it is running. But if the
configuration or environments increase it becomes difficult to manage them. So the real solution is to have them in 
the environment. This can be fixed by having more DevOps culture.


4. **Backing Services** - All backing services like MQ, or any other services should be easily interchangeable.
Like its path, connection parameters should be changeable & we should not be hardcoding them anywhere.

5. **Build, release, run** - Separation of these processes is important to make sure that automation and maintaining 
	the system will be as easy as possible.
	* Build - converting code repo into an executable bundle known as the build.
	* Release - getting the build and combining it with a config on a certain environment - ready to run. 
		This is also often referred to as deployment.
	* Run - starting the app in the deployment.

6. **Processes** - Applications should be deployed as one or more stateless processes with persisted data stored on a 
	backing service. The idea of stateless services, that can be easily scaled by deploying more of them is part 
	of the definition what a microservices are. You should not be introducing state into your services 
	(that should leave in database or memcached, redis - for the session information).
	
7. **Port binding** - Self-contained services should make themselves available to other services by specified ports.

8. **Concurrency** - Concurrency is advocated by scaling individual processes. The idea is that, as you need to 
scale, you should be deploying more copies of your application.

9. **Disposability** - Fast startup and shutdown are advocated for a more robust and resilient system.  It is 
important that they can go up and down quickly. Without this, automatic scaling and ease of deployment, 
development are being diminished. It also talks about crashes, your system should be fine even if 1 or more instances
die.

10. **Dev/Prod parity** - All environments should be as similar as possible.

11. **Logs** - Applications should produce logs as event streams and leave the execution environment to aggregate.
	Using Logstash/ELK can help with your logs.
	
12. **Admin Processes** - Any needed admin tasks should be kept in source control and packaged with the application.
Admin tasks should be run from the relevant servers- possibly production servers. This is easiest done by 
shipping admin code with application code to provide these capabilities. The tools should be there even if 
they are not part of the standard execution of the service.