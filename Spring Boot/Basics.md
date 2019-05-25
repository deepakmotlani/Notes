## Spring Boot

**What is Spring Boot?**
It is a kind of tool that lets you create standalone spring based applications.

Without Spring Boot, we have to do so many things to bring up the application i.e. import jars, do lot of 
configurations, Spring Boot takes care of all this things.

**Problems with Spring**
* Huge framework, as it provides support for almost everything needed to build an enterprise application.
* Lot of setup & configurations steps
* Lot of build & deployment steps

So Spring boot abstracts all these steps & handles majority of the use cases, for the rest you can do some tweaks.

**Spring Boot**
* Opinionated, means it makes certain configuration choices.
* Convention over Configuration, means it works for 80% use cases for 20% use cases you need to modify.
* Stand alone, when you use spring you will generally create a war file & deployt it on servlet container, but what	
	Spring Boot does is it creates a standalone application which you can directly run & you don't have to worry about
	servlet container etc.
* Production Ready, you don't have to do anything for making it production ready.

## Create Spring Boot application

1. Create a simple maven project, which will simply have pom.xml.

2. Now add parent project for this project in pom.xml. Parent project is going to be spring boot starter parent.
```
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>1.4.2.RELEASE</version>
</parent>
```
Adding a parent project is a concept of maven, what does this mean is we can copy configuration from parent project.
As soon as you declare spring-boot-starter-parent as parent, your application becomes Spring Boot application.
spring-boot-starter-parent contains all default configurations for spring boot application, i.e. all opinionated 
dependencies.

3. If you want to create a web application, then you need to add a dependency i.e. spring-boot-starter-web, now this
dependency is again provided by spring boot which is a meta dependency for all the dependencies required for building
a web project.

4. By default spring boot uses java 1.6, you can change the version by specifying
```
<properties>
	<java-version>1.8</java-version>
</properties>
```

5. Next we have to do is create a main class as below
```
@SpringBootApplication
public class SpringBoot {
	public static void main(String args[]) {
		SpringApplication.run(SpringBoot.class, args);
	}
}
```
This is pretty much, you can just run this main class & you will see that spring boot will run tomcat server on port
8080 & also deploy your application on it.
Now what is happening in b/g is SpringApplication.run method does following
 * Setup default configuration
 * Starts Spring application context
 * Performs classpath scan i.e. Service, Repository, Controller classes.
 * Starts Tomcat server.
That's why we say Spring Boot creates standalone application.

Parent Project version specifies which version of each dependency to use internally.

## Another way of creating spring boot applications is using Spring Initializer i.e. http://start.spring.io webpage. 

Goto this webpage & select the boot version, type of project i.e. maven/gradle, then mention the groupId &
artifactId & application name. You can also specify the dependencies you need by simple checkbox selection & then
click download, it should download a zip for you. Extract the zip & import the project in your IDE.

## Another way of creating spring boot application is by using Spring Boot CLI. 

We can download the CLI zip from spring official website, extract it & run. This is not very popuplar & is mainly
used for woking with groovy.

## Another way is using STS IDE
Create Spring Starter Project which is similar to spring initializer, but it downloads & extracts the project.