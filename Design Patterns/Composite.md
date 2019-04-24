### Composite
Compose objects into tree structure to represent whole hierarchies. 

In this pattern the client uses the component interface to interact with objects which are part of the composition. You can imagine the composite hierarchy as a tree where there are leaves and composites, and the requests are sent through this tree.

If the recipient of the call is a leaf then the request is handled directly in this leaf. If the recipient is a composite then this composite forwards the requests to its children, alternatively this composite can perform additional operations before and after forwarding.

Example
One good example for this pattern can be a company structure. For example the first entry point is the VP of Marketing who wants a new feature / software developed. So he (or she) calls up the VP of Software Development to implement this feature. The VP calls up the managers to give him a time/cost estimate. These managers forward this request to their managers or developers. When the responses get back they are returned until the VP of Software Development who answers the VP of Marketing.

Let’s define the common interface of Employee. This interface defines the methods each employee of the company has to implement.

```
public interface Employee {    
    String getName();
    
    void add(Employee e);
    
    void remove(Employee e);
    
    List<Employee> getEmployees();
    
    int estimateProject(String projectDescription);
}

public abstract class Manager implements Employee {
    List<Employee> employees = new ArrayList<>();
    String name;
    public Manager(String name) {
        this.name = name;
    }
    @Override
    public List<Employee> getEmployees() {
        return this.employees;
    }
    @Override
    public void add(Employee e) {
        if (e != null) {
            this.employees.add(e);
        }
    }
    @Override
    public void remove(Employee e) {
        if (e != null) {
            this.employees.remove(e);
        }
    }
    @Override
    public int estimateProject(String projectDescription) {
        if (this.employees.isEmpty()) {
            return 0;
        }
        return Math.round(this.employees.stream().mapToInt(e -> {
            System.out.println(e);
            return e.estimateProject(projectDescription);
        }).sum() / this.employees.size());
    }
    @Override
    public String getName() {
        return this.name;
    }
}

public class VP extends Manager {
    public VP(String name) {
        super(name);
    }
    @Override
    public String toString() {
        return "I am " + getName() + ", VP";
    }
    /**
     * VP doubles the estimated amount.
     */
    @Override
    public int estimateProject(String projectDescription) {
        System.out.println("I am " + getName() + ", the VP, and calling for an estimate...");
        final int projectEstimate = super.estimateProject(projectDescription);
        System.out.println("Original estimate: " + projectEstimate);
        return Math.toIntExact(Math.round(projectEstimate * 2));
    }
}

public class SeniorManager extends Manager {
    public SeniorManager(String name) {
        super(name);
    }
    /**
     * Senior Managers add 10% to the estimate of the team.
     */
    @Override
    public int estimateProject(String projectDescription) {
        return Math.toIntExact(Math.round(super.estimateProject(projectDescription) * 1.1));
    }
    @Override
    public String toString() {
        return "I am " + getName() + ", Senior Manager";
    }
}

public class TeamLeader extends Manager {
    public TeamLeader(String name) {
        super(name);
    }
    @Override
    public String toString() {
        return "I am " + getName() + ", Team Leader";
    }
}
public class Developer implements Employee {
    String name;
    public Developer(String name) {
        this.name = name;
    }
    @Override
    public String getName() {
        return this.name;
    }
    @Override
    public void add(Employee e) {
    }
    @Override
    public void remove(Employee e) {
    }
    @Override
    public List<Employee> getEmployees() {
        return null;
    }
    @Override
    public int estimateProject(String projectDescription) {
        return new Random().nextInt(24);
    }
    @Override
    public String toString() {
        return "I am " + getName() + ", Developer";
    }
}

```
Now let's implement a structure & see how it works
```
public class Composite {
    public static void main(String... args) {
        final Developer d1 = new Developer("Jack");
        final Developer d2 = new Developer("Jill");
        final Developer d3 = new Developer("Brian");
        final Developer d4 = new Developer("Bob");
        final Manager tl1 = new TeamLeader("Marc");
        final Manager tl2 = new TeamLeader("Christian");
        final Manager tl3 = new TeamLeader("Phil");
        tl1.add(d3);
        tl1.add(d2);
        tl2.add(d1);
        tl3.add(d4);
        final Manager sm1 = new SeniorManager("Harald");
        final Manager sm2 = new SeniorManager("Klaus");
        sm1.add(tl3);
        sm1.add(tl2);
        sm2.add(tl1);
        final VP vp = new VP("Joseph");
        vp.add(sm1);
        vp.add(sm2);
        System.out.println("Our estimate is: " + vp.estimateProject("New exotic feature"));
    }
}
```

**Output**
```
I am Joseph, the VP, and calling for an estimate…
I am Harald, Senior Manager
I am Phil, Team Leader
I am Bob, Developer
I am Christian, Team Leader
I am Jack, Developer
I am Klaus, Senior Manager
I am Marc, Team Leader
I am Brian, Developer
I am Jill, Developer
Original estimate: 9
Our estimate is: 18
```

This example shows how it goes down to each individual employee & gets the estimate.
