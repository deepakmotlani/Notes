### Adapter Pattern 
It is a structural design pattern that allows two unrelated/uncommon interfaces to work together. In other words, the adapter pattern makes two incompatible interfaces compatible without changing their existing code.
Interfaces may be incompatible, but the inner functionality should match the requirement.

Adapter Pattern use a single class (the adapter class) to join functionalities of independent or incompatible interfaces/classes.
This pattern converts the (incompatible) interface of a class (the adaptee) into another interface (the target) that clients require.

Example, lets consider that there is a UKPlug, UKSocket & IndianPlug, IndianSocket. Now if we want to use IndianPlug in UKSocket, we will have to create adapter for IndianPlug which will work with UKSocket.

```
class UKSocket {
  void giveElectricity(UKPlug plug){
    plug.giveElectricity();
  }
}

class UKPlug {
  void giveElectricity(){
    System.out.println('Giving electricity');
  }
}

class IndianSocket {
  void giveElectricity(IndianPlug plug){
    plug.giveElectricity();
  }
}

class IndianPlug {
  void giveElectricity(){
    System.out.println('Giving electricity');
  }
}

class IndianToUKPlugAdapter extends UKPlug {
  private IndianPlug plug;
  
  public IndianToUKPlugAdapter(IndianPlug plug){
    this.plug = plug;
  }
  
  void giveElectricity(){
    plug.giveElectricity();
  }
}

class TestClass {
  public static void main(String args[]){
    UKSocket socket = new UKSocket();
    IndianPlug plug = new IndianPlug();
    IndianToUKPlugAdapter adapter = new IndianToUKPlugAdapter(plug);
    socket.giveElectricity(adapter);
  }
}
```
