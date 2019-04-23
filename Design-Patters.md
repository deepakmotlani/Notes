## Design Patterns

**Singleton** - As per this pattern only 1 instance should be instantiated. 1 way to acheieve this is to make the contructor of the class private & have a static method which will create a single instance & return it to all the invokers.


**Factory** - Let's take an example that every application has to go through following phases i.e. development, testing & acceptance. Now this applications could be implemented on any OS i.e. iOS, Android, Windows etc. So in order to get the app of a particular type we create factory classes, i.e. separation of decision making into a separate class.

```
public static App createApp(AppType type) {
   App app;
   switch (type) {
   case IOS:
       app = new IOSApp();
       break;
   case TV:
      app = new TVApp();
       break;
   case GLASS:
       app = new GlassApp();
       break;
   default:
       app = new GlassApp();
       break;
   }
   return app;
}
```

**Decorator** - This is used when we want to have a default behaviour for all objects & have some special decorations on top of some objects & have some other decorations on others.

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
