### Dirty check
Hibernate uses a strategy called inspection, which is basically this: when an object is loaded from the database a snapshot of it is kept in memory. When the session is flushed Hibernate compares the stored snapshot with the current state. If they differ the object is marked as dirty and a suitable SQL command is enqueued. If the object is still transient then it is always dirty.

### Lazy Loading
Say you have a parent and that parent has a collection of children. Hibernate now can "lazy-load" the children, which means that it does not actually load all the children when loading the parent. Instead, it loads them when requested to do so. You can either request this explicitly or, and this is far more common, hibernate will load them automatically when you try to access a child. Lazy-loading can help improve the performance significantly since often you won't need the children and so they will not be loaded.

Also beware of the n+1-problem. Hibernate will not actually load all children when you access the collection. Instead, it will load each child individually. When iterating over the collection, this causes a query for every child. In order to avoid this, you can trick hibernate into loading all children simultaneously, e.g. by calling parent.getChildren().size().

### The differences between get() and load() methods are given below
get()	
Returns null if an object is not found.
Always hits the database.
It returns the real object, not the proxy.	
It should be used if you are not sure about the existence of instance.	

load()
Throws ObjectNotFoundException if an object is not found.
Doesn't hit the database.
It returns proxy object.
It should be used if you are sure that instance exists.

### The update() method	merge() method
update() should be used inside the session only. After closing the session, it will throw the error.	
merge() should be used if you don't know the state of the session, means you want to make the modification at any time.


### @EmbeddedId is used to instruct Hibernate that the Employee entity uses a compound key.
```
@Embeddable
public class EmployeeId implements Serializable {
    @Column(name = "company_id")
    private Long companyId;
 
    @Column(name = "employee_number")
    private Long employeeNumber;
 
    public EmployeeId() {
    }
 
    public EmployeeId(Long companyId, Long employeeId) {
        this.companyId = companyId;
        this.employeeNumber = employeeId;
    }
 
    public Long getCompanyId() {
        return companyId;
    }
 
    public Long getEmployeeNumber() {
        return employeeNumber;
    }
 
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof EmployeeId)) return false;
        EmployeeId that = (EmployeeId) o;
        return Objects.equals(getCompanyId(), that.getCompanyId()) &&
                Objects.equals(getEmployeeNumber(), that.getEmployeeNumber());
    }
 
    @Override
    public int hashCode() {
        return Objects.hash(getCompanyId(), getEmployeeNumber());
    }
}

@Entity(name = "Employee")
@Table(name = "employee")
public class Employee {
    @EmbeddedId
    private EmployeeId id;
 
    private String name;
 
    public EmployeeId getId() {
        return id;
    }
 
    public void setId(EmployeeId id) {
        this.id = id;
    }
 
    public String getName() {
        return name;
    }
 
    public void setName(String name) {
        this.name = name;
    }
}
```
In this example the Employee entity has composite key.


### Hibernate Caching -

**First Level Cache** - Also called session cache & it is mandatory. It is from first level cache that all requests should pass. Session object stores an object under its control before committing it to db. When session object is closed the cached objects are gone. Whenever a query is executed the results are retrieved from db & stored in session cache, if we execute the same query next time within the same session, it will return the results from cache & not hit the database. Loaded entity can removed from session using evict() method, whole session can be removed using clear() method.

**Second Level Cache** - It is an optional cache, it is implemented at class level. It stores the entity data but not the entity. Data is stored in dehydrated format in hashmap, where key is entity id & value is list of primitive values. It is used to cache the data across sessions. It is associated with SessionFactory. It is not enabled by default.

*-----------------------------------------*
|          Person Data Cache              |
|-----------------------------------------|
| 1 -> [ "John" , "Q" , "Public" , null ] |
| 2 -> [ "Joey" , "D" , "Public" ,  1   ] |
| 3 -> [ "Sara" , "N" , "Public" ,  1   ] |
*-----------------------------------------*

**Query Cache**, looks like an hashmap where key is composed by query text & values & value is list of entity id's.

*----------------------------------------------------------*
|                       Query Cache                        |                     
|----------------------------------------------------------|
| ["from Person where firstName=?", ["Joey"] ] -> [1, 2] ] |
*----------------------------------------------------------*

If a query under execution has previously cached results, then no SQL statement is sent to the database. Instead the query results are retrieved from the query cache, and then the cached entity identifiers are used to access the second level cache.

If the second level cache contains data for a given Id, it re-hydrates the entity and returns it. If the second level cache does not contain the results for that particular Id, then an SQL query is issued to load the entity from the database.
