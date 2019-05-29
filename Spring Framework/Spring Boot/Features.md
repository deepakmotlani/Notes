## Spring Boot Features

### 1. Auto Configuration
If you have worked on a normal Spring application which makes use of JdbcTemplate to connect to H2 database. You will have to a lot of
configuration i.e. creating a Datasource, JdbcTemplate. You can avoid doing all these if you are using Spring Boot, because it does a lot 
of **Auto Configuration** for us. If you have added the JdbcTemplate & H2.jar in your classpath, Spring Boot will automatically create 
JdbcTemplate for your H2 database, you can simply start using JdbcTemplate in your classes.

Spring Boot does 200+ such **Auto Configurations** & configures many dependencies by looking at classpath dependencies.

Auto Configuration is by default disabled & you can enable it using **@EnableAutoConfiguration** or **@SpringBootApplication**.
