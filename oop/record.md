# Record

A _Java_ _Record_ is a special kind of Java class which has a concise syntax for defining immutable data-only classes.&#x20;

Uuseful for holding records returned from a database query, records returned from a remote service call, records read from a CSV file, or similar types of use cases.

A Java Record consist of one or more data fields which corresponds to member variables in a regular Java class. The Java compiler auto generates getter methods, toString(), [hashcode() and equals() methods](https://jenkov.com/java-collections/hashcode-equals.html) for these data fields, so you don't have to write that boilerplate code yourself.&#x20;

{% hint style="warning" %}
Since a Java Record is immutable, no setter methods are generated
{% endhint %}

{% hint style="warning" %}
A Record type definition is final, meaning you cannot create subclasses (subrecords) of a Java Record type
{% endhint %}

```
public record Vehicle(String brand, String licensePlate) {}

public class RecordsExample {

  public static void main(String[] args) {

    Vehicle vehicle = new Vehicle("Mercedes", "UX 1238 A95");

    System.out.println( vehicle.brand() ); // auto generated
    System.out.println( vehicle.licensePlate() ); // auto generated
    System.out.println( vehicle.toString() ); // auto generated

  }
}
```

### Multiple Constructor



```
public record Vehicle(String brand, String licensePlate) {

    public Vehicle(String brand) {
        this(brand, null);
    }

}
```

### Methods



```
public record Vehicle(String brand, String licensePlate) {
    
    // instance method
    public String brandAsLowerCase() {
        return brand().toLowerCase();
    }
    
    // static method
        public static String brandAsUpperCase(Vehicle vehicle) {
        return vehicle.brand.toUpperCase();
    }
}
```
