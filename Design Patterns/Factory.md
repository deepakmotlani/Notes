### Factory
Let's take an example that every application has to go through following phases i.e. development, testing & acceptance. Now this applications could be implemented on any OS i.e. iOS, Android, Windows etc. So in order to get the app of a particular type we create factory classes, i.e. separation of decision making into a separate class. Applicable only if the parent type is common for all sub types

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