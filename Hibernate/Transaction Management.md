## Transaction Management

Transaction is associated with a session object in hibernate. Transation is a unit of work.

Example - 

```
Session session = null;  
Transaction tx = null;  
  
try {  
	session = sessionFactory.openSession();  
	tx = session.beginTransaction();  
	//I will perform all the operations here  
	  
	tx.commit();    
}catch (Exception ex) {  
	ex.printStackTrace();  
	tx.rollback();  
}  
finally {
	session.close();
}  
```

## With Spring Boot

1. Specify datasource & hibernate properties in property file.
2. Create a configuration class where we will create DataSource, Session Factory & Transation Manager beans.
```
@Bean(name = "dataSource")
public DataSource getDataSource() {
	DriverManagerDataSource dataSource = new DriverManagerDataSource();
	 
	dataSource.setDriverClassName(env.getProperty("spring.datasource.driver-class-name"));
	dataSource.setUrl(env.getProperty("spring.datasource.url"));
	dataSource.setUsername(env.getProperty("spring.datasource.username"));
	dataSource.setPassword(env.getProperty("spring.datasource.password"));

	System.out.println("## getDataSource: " + dataSource);

	return dataSource;
}
@Autowired
@Bean(name = "sessionFactory")
public SessionFactory getSessionFactory(DataSource dataSource) throws Exception {
	Properties properties = new Properties();
	
	properties.put("hibernate.dialect", env.getProperty("spring.jpa.properties.hibernate.dialect"));
	properties.put("hibernate.show_sql", env.getProperty("spring.jpa.show-sql"));
	properties.put("current_session_context_class", //
			env.getProperty("spring.jpa.properties.hibernate.current_session_context_class"));

	LocalSessionFactoryBean factoryBean = new LocalSessionFactoryBean();

	factoryBean.setPackagesToScan(new String[] { "" });
	factoryBean.setDataSource(dataSource);
	factoryBean.setHibernateProperties(properties);
	factoryBean.afterPropertiesSet();

	SessionFactory sf = factoryBean.getObject();
	System.out.println("## getSessionFactory: " + sf);
	return sf;
}
 
@Autowired
@Bean(name = "transactionManager")
public HibernateTransactionManager getTransactionManager(SessionFactory sessionFactory) {
	HibernateTransactionManager transactionManager = new HibernateTransactionManager(sessionFactory);

	return transactionManager;
}
```
3. Next you can use @Transactional with your service or dao methods.

**@Transactional** attributes
* value = alias for transaction manager
* timeout = int timeout for this transaction
* rollbackFor = Defines 0 or more exception classes for which transaction should rollback
* propogation has following possible values
	* MANDATORY - Supports current transaction, throw exception if none exists.
	* REQUIRED - Supports current transaction, create new if none exists.
	* REQUIRES_NEW - Create new transaction & suspend current transaction.
	* NEVER - Execute non transactionally.
* isolation has following possible values
	* READ_COMMITTED - Doesn't allow dirty read
	* READ_UNCOMMITTED - Allow Dirty reads
	* REPEATABLE_READ - If row is read twice in transaction, result will be always same
	* SERIALIZABLE - Performs all transactions in sequence