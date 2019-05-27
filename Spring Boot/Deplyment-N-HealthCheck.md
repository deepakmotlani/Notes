## Deploying

By default Spring Boot creates a jar file in the terget directory, which we can simply run from command prompt using
below command.
```
java -jar abc.jar
```

This will start as an application because it contains embedded Tomcat, which will start on 8080.

Now suppose that you already have a tomcat & you don't want to use embedded one, you can goto pom.xml & specify
```
<packaging>war</packaging>
```

So when you run mvn clean install this will rather give you a war file which you can take to any tomcat instance &
deploy.

## Health Check

Spring Boot provides actuator dependency, which gives lot of reports of your application regarding health.

As soon as you add this dependency, you will get lot of endpoints which gives so many details of your application.

1. /health - It provides you information like diskSpace, freeSpace etc.
2. /beans - provides you a list of all the beans in your application with their dependencies.

And many more.