### Builder Pattern 
says that "***construct a complex object from simple objects using step-by-step approach***". It is mostly used when object can't be created in single step.

Lets consider an example of ***Order*** which we place at hotel. So we place order for items 1 by 1 i.e. Veg Cheese Pizza Small Size & Coke Large Size & more items as per our need. So in order to create this order we should use builder pattern.

In this example you can see that, we have an item interface, which is implemented by Pizza & Coke abstract classes, which are further extended by Veg Pizza, Non-Veg Pizza, Coke & Pepsi abstract classes respectively. Continuing futher till the actual concrete classes i.e. SmallCheese, MediumCheese, LargeCheese, ExtraLargeCheese likewise for Coke & Pepsi.

You have OrderedItems class which has addItems(Item) method which accepts items. It also gives 2 more methods the getCost() of all ordered items & showItems() which prints list of all items ordered.

You also have an OrderBuilder class which has a list of OrderedItems & 2 methods preparePizza() which takes your choices of pizza & add those to OrderedItems list & prepareColdrink() which takes your choice of coldrink & add it to OrderedItems list.

So this way you build your Order object in multiple steps.

![](https://github.com/deepakmotlani/Notes/blob/master/Design%20Patterns/images/builder.jpg)
