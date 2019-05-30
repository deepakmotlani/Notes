## Spring Boot Features

### 1. Auto Configuration
If you have worked on a normal Spring application which makes use of JdbcTemplate to connect to H2 database. You will have to a lot of
configuration i.e. creating a Datasource, JdbcTemplate. You can avoid doing all these if you are using Spring Boot, because it does a lot 
of **Auto Configuration** for us. If you have added the JdbcTemplate & H2.jar in your classpath, Spring Boot will automatically create 
JdbcTemplate for your H2 database, you can simply start using JdbcTemplate in your classes.

Spring Boot does 200+ such **Auto Configurations** & configures many dependencies by looking at classpath dependencies.

Auto Configuration is by default disabled & you can enable it using **@EnableAutoConfiguration** or **@SpringBootApplication**.

### 2. Starter POMs
Takes away the pain of finding & adding dependencies to your project. In order to develop a Spring MVC applications with Rest & Jackson, you would need following jars -
1. spring-core.jar
2. spring-web.jar
3. spring-webmvc.jar
4. jackson-databind.jar
5. tomcat-embed-core.jar
6. tomcat-embed-el.jar
7. tomcat-embed-logging-juil.jar

By using Spring Boot starter dependency, you can get all of these jars by just adding **spring-boot-starter-web** dependency in your application. So this takes away the pain of searching all the jars & their compatible versions, you can just add starter dependency & you are done. Similarly there are so many starter dependencies i.e. **spring-boot-starter-jdbc**, **spring-boot-starter-test**.

### 3. Actuator
This is an awesome feature of Spring Boot that helps us seeing what's going inside our application. Using this we can get insights & metrics of our application like, 

* How many beans are configured in application-context? /beans
* What are environment variables? /env
* What are system properties?
* What are command-line args?
* CPU & Memory usage.
* Health - /health

All these information is provided by various endpoints provided by Actuator. But 1 thing dangerous here is that this endpoints are not secure, so we should secure these endpoints using spring security.

### 4. Spring Boot Initializer
Spring Boot Initializer provides a web application i.e. https://start.spring.io, where you can create Maven & Gradle projects, project meta-data i.e. group Id, artifact Id, boot version & most importantly all the dependencies needed. Once you are done configuring all these, click Generate Project, which generates a .zip file which will be downloaded, you can extract & import it.

### 5. Spring Boot CLI
Spring Boot Command Line Interface, is used for quick start with Spring. It can run groovy scripts, & avoids developers to write boiler plate code & focus on business logic.

Provides interface to test & run applications from commnd-prompt. 
