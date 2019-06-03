## Arguement Matchers

When adding behaviour we have to specify parameters of method like below
```
Mockito.when(calcService.add(10, 20)).thenReturn(30);
```

But we may want to work for broader range of parameters, that can be done by Arguement Matchers, like below
```
Mockito.when(calcService.add(Matchers.anyInt(), Matchers.anyInt())).thenReturn(30);
```
Using this we specify that for any integer parameters, we want to return 30.

**Matchers is provided by org.mockito package.**
* Can't be used in return arguements.
* Can't be used outside of verification or stubbing.

Incorrect example
```
String orMatcher = Mockito.or(Mockito.eq("poppy"), Mockito.endsWith("y"));
Mockito.verify(mock).analyze(orMatcher);
```

Correct example
```
Mockito.verify(mock).analyze(Mockito.or(Mockito.eq("poppy"), Mockito.endsWith("y")));
```

Mockito provides additional matchers to implement common logical operations (not, and, or)
