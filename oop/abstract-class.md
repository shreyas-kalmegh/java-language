# Abstract Class

A _Java abstract class_ is a class which cannot be instantiated, meaning you cannot create new instances of an abstract class. The purpose of an abstract class is to function as a base for subclasses.



```
public abstract class MyAbstractClass {
    public abstract void abstractMethod();
}

public class MySubClass extends MyAbstractClass {
    public void abstractMethod() {
        System.out.println("My method implementation");
    }
}
```

An abstract method has no implementation. It just has a method signature. Just like methods in a [Java interface](https://jenkov.com/tutorials/java/interfaces.html).

If a class has an abstract method, the whole class must be declared abstract. Not all methods in an abstract class have to be abstract methods. An abstract class can have a mixture of abstract and non-abstract methods.

Subclasses of an abstract class must implement (override) all abstract methods of its abstract superclass. The non-abstract methods of the superclass are just inherited as they are. They can also be overridden, if needed.

### The Purpose of Abstract Classes

The purpose of abstract classes is to function as base classes which can be extended by subclasses to create a full implementation. For instance, imagine that a certain process requires 3 steps:

1. The step before the action: implementation in abstract class
2. The action.: implementation in subclass
3. The step after the action.: implementation in abstract class
4.

    ```
    public abstract class MyAbstractProcess {

        public void process() {
            stepBefore();
            action();
            stepAfter();
        }

        public void stepBefore() {
            //implementation directly in abstract superclass
        }

        public abstract void action(); // implemented by subclasses

        public void stepAfter() {
            //implementation directly in abstract superclass
        }
    }
    ```

{% hint style="info" %}
You can make a superclass abstract, even if it contains no abstract methods.
{% endhint %}

#### Abstract Classes and the Template Method Design Pattern

The Template Method design pattern provides a partial implementation of some process, which subclasses can complete when extending the Template Method base class.
