## SOLID design principle

1. **Single Responsibility Principle** - A class should only have a single responsibility, that is, only changes 
	to one part of the software's specification should be able to affect the specification of the class. For ex-
	If there is a report generation software, now there is a change report content and report format, now bothe these
	are seperate concerns i.e. data & conmetic, so they should be in seperate classes. It would be a ad design to
	couple them together.

2. **Open–closed principle** - "Software entities should be open for extension, but closed for modification."
	A module will be said to be open if it is still available for extension. For example, it should be possible 
		to add fields to the data structures it contains, or new elements to the set of functions it performs.
	A module will be said to be closed if it is available for use by other modules. This assumes that the module 
		has been given a well-defined, stable description.

3. **Liskov substitution principle** - 
		
4. **Interface segregation principle** - Interface-segregation principle (ISP) states that no client should be 
	forced to depend on methods it does not use. ISP splits interfaces that are very large into smaller and more 
	specific ones so that clients will only have to know about the methods that are of interest to them. 
	Such shrunken interfaces are also called role interfaces. ISP is intended to keep a system decoupled and 
	thus easier to refactor, change, and redeploy.

5. **Dependency inversion principle** - High level modules should not depend on Low level modules, both should 
	depend on abstractions.

Ex - 
```
public class BackEndDeveloper {
    public void writeJava() {
    }
}

public class FrontEndDeveloper {
    public void writeJavascript() {
    }
}

public class Project {
    private BackEndDeveloper backEndDeveloper = new BackEndDeveloper();
    private FrontEndDeveloper frontEndDeveloper = new FrontEndDeveloper();
    public void implement() {
        backEndDeveloper.writeJava();
        frontEndDeveloper.writeJavascript();
    }
}
```

So as we can see, the Project class is a high-level module, and it depends on low-level modules such as 
	BackEndDeveloper and FrontEndDeveloper. Also the implement method of Project calls methods bound to 
	corresponding classes. So in order to avoid this, we shall implement it like

```
public interface Developer {
    void develop();
}

public class BackEndDeveloper implements Developer {
    @Override
    public void develop() {
        writeJava();
    }
    private void writeJava() {
    }
}

public class FrontEndDeveloper implements Developer {
    @Override
    public void develop() {
        writeJavascript();
    }
    public void writeJavascript() {
    }
}

public class Project {
    private List<Developer> developers;
    public Project(List<Developer> developers) {
        this.developers = developers;
    }
    public void implement() {
        developers.forEach(d->d.develop());
    }
}
```

So the outcome is that Project class is not dependent on lower level classes, but abstractions.