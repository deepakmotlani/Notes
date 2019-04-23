### Decorator
This is used when we want to have a default behaviour for all objects & have some special decorations on top of some objects & have some other decorations on others.

```
public interface App {    
    void developApp(); //this is the behaviour which we want to decorate
}

public class IOSApp implements App {
    @Override
    public void developApp() { //providing default behaviour
        System.out.println("Developing an iOS app");
    }
}

public abstract class AppDecorator implements App {    
    App delegate; // decorator which holds object to be decorated
}

public class TVAppDecorator extends AppDecorator {    
    public TVAppDecorator(App delegate) {
        this.delegate = delegate;
    }
    @Override
    public void developApp() { //decorating the behvaiour for TV
        this.delegate.developApp();
        System.out.println("Adding TV extension...");
    }
}

public class WatchAppDecorator extends AppDecorator {    
    public WatchAppDecorator(App delegate) {
        this.delegate = delegate;
    }
    @Override
    public void developApp() { //decorating the behvaiour for Watch
        this.delegate.developApp();
        System.out.println("Adding Watch extension...");
    }
}

public class AppStore {
    public static void main(String... args) {
        final App tvApp = new TVAppDecorator(new IOSApp()); //here we take the original object & then use TV decorator on top of it
        tvApp.developApp();
        
        final App watchApp = new WatchAppDecorator(new IOSApp()); //here we take the original object & then use Watch decorator on top of it
        watchApp.developApp();
    }
}
```
