## HQL

Hibernate Query Language is same as SQL just that we use class names instead of table name, that's why it is independent
of database.

Query interface is an object representation of query. Query can be created using createQuery() method of 
Session interface.

* Get list of objects
```
Query query = session.createQuery('from Employee');
List employees = query.list();
```

* Get list of objects with pagination
```
Query query = session.createQuery('from Employee');
query.setFirstResult(5);
query.setMaxResult(10);
List employees = query.list();
```

* Update query
```
Query q = session.createQuery("update User set name=:n where id=:i");  
q.setParameter("n","Udit Kumar");  
q.setParameter("i",111);  
  
int status=q.executeUpdate();  
```

* Get sum of all salaries
```
Query q=session.createQuery("select sum(salary) from Emp");  
List<Integer> list=q.list();  
System.out.println(list.get(0)); 
```

## Criteria

* Get list of all employees
```
Criteria criteria =  session.createCriteria(Employee.class);
List employees = criteria.list();
```

* Pagination
```
Criteria criteria =  session.createCriteria(Employee.class);
criteria.setFirstResult(10);
criteria.setMaxResult(20);
List employees = criteria.list();
```

* Apply restrictions to get records whole salary is greater than 10000
```
Criteria criteria =  session.createCriteria(Employee.class);
criteria.add(Restrictions.gt("salary", 10000)); // where salary is property name
List employees = criteria.list();
```
Restrictions provides several such methods i.e. lt, le, ge, eq, ne, between & like.

* Order by salary
```
Criteria criteria =  session.createCriteria(Employee.class);
criteria.add(Order.asc("salary")); 
List employees = criteria.list();
```
Order provides 2 methods i.e. asc & desc.

* Fetch specific columns
```
Criteria criteria =  session.createCriteria(Employee.class);
criteria.setProjection(Projections.property("salary")); 
List employees = criteria.list();
```