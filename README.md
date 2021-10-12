# CreationalDP
# Author: Corman Daniel
Objectives :
1. Study the Creational Design Patterns

2. Implement them in real projects

Theory :
In software engineering, creational design patterns are design patterns that deal with object creation mechanisms, trying to create objects in a manner suitable to the situation.

The basic form of object creation could result in design problems or added complexity to the design. Creational design patterns solve this problem by somehow controlling this object creation.

Some examples of this kind of design patterns are :

Singleton
Builder
Prototype
Object Pooling
Factory Method
Abstract Factory
Implementation :
In this project I've implemented 3 creational design patterns i.e. ( Builder,  Factory Method and Abstract Factory) with the emphasis on the fundamental object Car.
...

enum CarType
{
    MICRO, MINI, LUXURY
}
  
abstract class Car
{
    Car(CarType model, Location location)
    {
        this.model = model;
        this.location = location;
    }
   
    abstract void construct();
   
    CarType model = null;
    Location location = null;
   
    CarType getModel()
    {
        return model;
    }
   
    void setModel(CarType model)
    {
        this.model = model;
    }
   
    Location getLocation()
    {
        return location;
    }
   
    void setLocation(Location location)
    {
        this.location = location;
    }
   
    @Override
    public String toString()
    {
        return "CarModel - "+model + " located in "+location;
    }
}
  
class LuxuryCar extends Car
{
    LuxuryCar(Location location)
    {
        super(CarType.LUXURY, location);
        construct();
    }
    @Override
    protected void construct()
    {
        System.out.println("Connecting to luxury car");
    }
}
  
class MicroCar extends Car
{
    MicroCar(Location location)
    {
        super(CarType.MICRO, location);
        construct();
    }
    @Override
    protected void construct()
    {
        System.out.println("Connecting to Micro Car ");
    }
}
  
class MiniCar extends Car
{
    MiniCar(Location location)
    {
        super(CarType.MINI,location );
        construct();
    }
      
    @Override
    void construct()
    {
        System.out.println("Connecting to Mini car");
    }
}
  
enum Location
{
  DEFAULT, USA, INDIA
}
  
class INDIACarFactory
{
    static Car buildCar(CarType model)
    {
        Car car = null;
        switch (model)
        {
            case MICRO:
                car = new MicroCar(Location.INDIA);
                break;
              
            case MINI:
                car = new MiniCar(Location.INDIA);
                break;
                  
            case LUXURY:
                car = new LuxuryCar(Location.INDIA);
                break;
                  
                default:
                break;
              
        }
        return car;
    }
}
  
class DefaultCarFactory
{
    public static Car buildCar(CarType model)
    {
        Car car = null;
        switch (model)
        {
            case MICRO:
                car = new MicroCar(Location.DEFAULT);
                break;
              
            case MINI:
                car = new MiniCar(Location.DEFAULT);
                break;
                  
            case LUXURY:
                car = new LuxuryCar(Location.DEFAULT);
                break;
                  
                default:
                break;
              
        }
        return car;
    }
}
  
  
class USACarFactory
{
    public static Car buildCar(CarType model)
    {
        Car car = null;
        switch (model)
        {
            case MICRO:
                car = new MicroCar(Location.USA);
                break;
              
            case MINI:
                car = new MiniCar(Location.USA);
                break;
                  
            case LUXURY:
                car = new LuxuryCar(Location.USA);
                break;
                  
                default:
                break;
              
        }
        return car;
    }
}
  
  
  
class CarFactory
{
    private CarFactory() 
    {
          
    }
    public static Car buildCar(CarType type)
    {
        Car car = null;
        
        Location location = Location.INDIA; 
          
        switch(location)
        {
            case USA:
                car = USACarFactory.buildCar(type);
                break;
                  
            case INDIA:
                car = INDIACarFactory.buildCar(type);
                break;
                      
            default:
                car = DefaultCarFactory.buildCar(type);
  
        }
          
        return car;
  
    }
}
public class AbstractDesign {
	  public static void main(String[] args)
	    {
	        System.out.println(CarFactory.buildCar(CarType.MICRO));
	        System.out.println(CarFactory.buildCar(CarType.MINI));
	        System.out.println(CarFactory.buildCar(CarType.LUXURY));
	    }
}
...
