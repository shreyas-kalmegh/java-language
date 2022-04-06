# Inheritance

Another commonly used term for inheritance is _specialization_ and _generalization_. A subclass is a specialization of a superclass, and a superclass is a generalization of one or more subclasses.

### What is inherited?

When a subclass extends a superclass in Java, all `protected` and `public` fields and methods of the superclass are inherited by the subclass. By _inherited_ is meant that these fields and methods are part of of the subclass, as if the subclass had declared them itself. `protected` and `public` fields can be called and referenced just like the methods declared directly in the subclass.

Fields and methods with default (package) access modifiers can be accessed by subclasses only if the subclass is located in the same package as the superclass



```
public class Vehicle {
    protected String licensePlate = null;

    public void setLicensePlate(String license) {
        this.licensePlate = license;
    }
}
public class Car extends Vehicle {
    int numberOfSeats = 0;

    public String getNumberOfSeats() {
        return this.numberOfSeats;
    }
}
```

### Type Casting

It is possible to reference a subclass as an instance of one of its superclasses.

```
Car     car     = new Car();
Vehicle vehicle = car;
```

#### Upcasting and Downcasting

You can always cast an object of a subclass to one of its superclasses. This is referred to as _upcasting_

It may also be possible to cast an object from a superclass type to a subclass type, but only if the object really is an instance of that subclass (or an instance of a subclass of that subclass). This is referred to as _downcasting_

__

```
Car     car     = new Car();

// upcast to Vehicle
Vehicle vehicle = car;

// downcast to car again
Car     car2    =  (Car) vehicle;
```

#### _Invalid downcasting_

__

```
Truck   truck   = new Truck();

// upcast to Vehicle
Vehicle vehicle = truck;

// downcast to car again
Car     car     =  (Car) vehicle;
```

### _Overriding Methods_

To override a method the method signature in the subclass must be the same as in the superclass. That means that the method definition in the subclass must have exactly the same name and the same number and type of parameters, and the parameters must be listed in the exact same sequence as in the superclass. Otherwise the method in the subclass will be considered a separate method.



```
public class Vehicle {
    String licensePlate = null;

    public void setLicensePlate(String licensePlate) {
        this.licensePlate = licensePlate;
    }
}
public class Car extends Vehicle {
    public void setLicensePlate(String license) {
        this.licensePlate = license.toLowerCase();
    }

}
```

If you override a method in a subclass, and the method is all of a sudden removed or renamed or have its signature changed in the superclass, the method in the subclass no longer overrides the method in the superclass. To make compiler complain if this happens



```
public class Car extends Vehicle {

    @Override
    public void setLicensePlate(String license) {
        this.licensePlate = license.toLowerCase();
    }

}
```

### Calling Super Class Method(overrided)

Use super

```
public class Car extends Vehicle {

    public void setLicensePlate(String license) {
        super.setLicensePlate(license);
    }

}
```

### Instance Of

The `instanceof` instruction can also be used determine if an object is a instance of a superclass of its class. Here is an `instanceof` example that checks if a `Car` object is an instance of `Vehicle`:



```
Car car = new Car();

boolean isVehicle = car instanceof Vehicle; // true
```

### Fields and inheritance

in Java fields cannot be overridden in a subclass

If, however, the subclass calls up into a method in the superclass, and that method accesses the field with the same name as in the subclass, it is the field in the superclass that is accessed.



```
public class Vehicle {

    String licensePlate = null;

    public void setLicensePlate(String licensePlate) {
        this.licensePlate = licensePlate;
    }

    public String getLicensePlate() {
        return licensePlate;
    }
}
public class Car extends Vehicle {

    protected String licensePlate = null;

    @Override
    public void setLicensePlate(String license) {
        super.setLicensePlate(license); // access Vehicle class field
    }

    @Override
    public String getLicensePlate() {
        return super.getLicensePlate(); // access Vehicle class field
    }

    public void updateLicensePlate(String license){
        this.licensePlate = license; // access Car class field
    }
}
```

### Constructor

The Java inheritance mechanism does not include constructors. In other words, constructors of a superclass are not inherited by subclasses. Subclasses can still call the constructors in the superclass using the `super()` contruct. In fact, a subclass constructor is required to call one of the constructors in the superclass as the very first action inside the constructor body

Java implicitly calls no arg super constructer if not explicitely defined

### Nested Classes

The same Java inheritance rules apply to [nested classes](https://jenkov.com/tutorials/java/nested-classes.html). Nested classes which are declared `private` are not inherited. Nested classes with the default (package) access modifier are only accessible to subclasses if the subclass is located in the same package as the superclass. Nested classes with the `protected` or `public` access modifier are always inherited by subclasses.

### Final Classes

A `final` class cannot be extended. In other words, you cannot inherit from a `final` class in Java.
