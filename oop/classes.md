# Classes

### Class

A Java class is a single, coherent unit of Java code which belongs together. A Java class may contain a mix of data (variables) and actions (methods).



```
public class MyClass {

}
```

Java files should be named the same as the name of the class they contain, with the `.java` as file name extension.

{% hint style="warning" %}
While we can keep multiple classes inside a single file  as long as one of them is public, **Only** put a **single class** definition in **each Java file**, unless your class contains inner classes of some kind.
{% endhint %}

### Constructor

A Java class can have a constructor. A constructor is a special method that is called when an object of the given class is created. The purpose of a constructor is to initialize the fields in the class.



```
public class Car {

    public String brand = null;
    
    // constructor #1
    public Car() {
    }
    
    // constructor #2
    public Car(String theBrand, String theModel, String theColor) {
        this.brand = theBrand;
    }

}
```

{% hint style="info" %}
You don't have to define a constructor for a class, but if you don't define any constructor, the Java compiler will insert a default, no-argument constructor for you
{% endhint %}

#### Constructor Overloading

A class can have multiple constructors, as l**ong as their signature (the parameters they take) are not the same**. You can define as many constructors as you need. When a Java class contains multiple constructors, we say that the constructor is overloaded (comes in multiple versions

#### Constructor Parameter

By default, if a parameter (or local variable) has the same name as a field in the same class, the parameter (or local variable) "shadows" for the field

{% hint style="info" %}
Use **this.** when parameter and field name are same. Otherwise it is not necessary
{% endhint %}

```
public class Employee {
    private String firstName = null;
    private String lastName  = null;
    
    public Employee(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName  = lastName;
    }
    
}
```

#### Call Constructor in Constructor



```
public class Employee {

    private String firstName = null;
    private int    birthYear = 0;

    public Employee(String first, int  year) {
        firstName = first;
        birthYear = year;
    }

    public Employee(String first, String last){
        this(first, -1);
    }
}
```

#### Call Constructor in Super Class



```
public class Vehicle {
    private String regNo = null;

    public Vehicle(String no) {
        this.regNo = no;
    }
}
public class Car extends Vehicle {    
private String brand = null;    
public Car(String br, String no) {
    // call constructor of super class
    super(no);
    this.brand = br;
   }
}
```

{% hint style="warning" %}
In case an exception is thrown from the `Car` constructor, the `car` variable will never be assigned a reference to the `Car` object you are trying to create. The `car` variable will still point to null.
{% endhint %}

### Object

A Java class is a template for how **objects** of that class looks. In other words, the `Car` class in the previous section is a template for how `Car` objects look



```
Car car1 = new Car();
Car car2 = new Car();

car1.setColor("red");
car2.setColor("green");
```

### Fields

A Java field is a variable inside a class.



```
[access_modifier] [static] [final] type name [= initial value] ;
```

#### Initial Value

A Java field can have be given an initial value. This value is assigned to the field when the field is created in the JVM.&#x20;

Static fields are created when the class is loaded. A class is loaded the first time it is referenced in your program.

&#x20;Non-static fields are created when the object owning them are created.

```
public class Customer {
    String customerType = "OnlineCustomer";
}
```

### Access Modifiers



* private: The `private` access modifier means that only code inside the class itself can access this Java field.
* package: The `package` access modifier means that only code inside the class itself, or other classes in the same package, can access the field. This is the default access modifier
* protected: The `protected` access modifier is like the `package` modifier, except subclasses of the class can also access the field, even if the subclass is not located in the same package.
* public: The `public` access modifier means that the field can be accessed by all classes in your application.

### Static and Non-static

A static field belongs to the class. Thus, no matter how many objects you create of that class, there will only exist one field located in the class, and the value of that field is the same, no matter from which object it is accessed

Non-static Java fields, on the other hand, are located in the instances of the class. Each instance of the class can have its own values for these fields.

### Final

A Java field can be declared `final`. A `final` field cannot have its value changed, once assigned. You declare a field to be `final` by adding the `final` keyword to the field declaration

We can declare a method as final, **once you declare a method final it cannot be overridden**. So, you cannot modify a final method from a sub class

### Methods

Java methods are similar to what is called functions or procedures in other programming languages

```
public MyClass{

    public void writeText(String text) {
        System.out.print(text);   //prints the text parameter to System.out.
    }
}
```

#### Parameters vs. Variables

A method parameter similar to a variable. You can read its value, and change its value too. Here is an example of a method changes the values of its parameters:



```
public MyClass{

    public void writeText(String text1, String text2) {
        text1 = "new value 1";      // change value of text1
        text2 = "new value 2";      // change value of text2
    }
}
```

{% hint style="warning" %}
Though it is possible to change the value of parameters, you should be careful doing that, as it may lead to confusing code.
{% endhint %}

#### Final Parameters

A Java method parameter can be declared `final`, just like a variable. The value of a `final` parameter cannot be changed. That is, if the parameter is a reference to an object, we cannot reassign the parameter, but values inside the object can still be changed.

#### Return Multiple Values

we can return multiple values by declaring a class and creating an object with all the return values.

or we can return them in a container object like array/list/map etc

or we can use a record class object which is like a dataclass in python, a class which is meant to hold only data

#### Exception Declaration



If an error occurs inside a method, the method may throw an exception. Exceptions have to be declared in the method declaration, like this (marked in bold):

```
public String concat(String string1, String string2) throws MyException {

    if(string1 == null) {
        throw new MyException("string1 was null");
    }
    if(string2 == null) {
        throw new MyException("string2 was null");
    }

    return string1 + string2;
}
```

{% hint style="info" %}
When an exception is thrown, the method also stops executing. But, instead of returning to where the method was called from, the execution is resumed inside the first `catch() { }` clause surrounding the method, targeted at that exception.
{% endhint %}
