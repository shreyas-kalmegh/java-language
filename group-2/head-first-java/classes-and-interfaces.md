# Classes and Interfaces

### Minimize the accessibility of classes and members

* make each class or member as inaccessible as possible
* Instance fields of public classes should rarely be public
* classes with public mutable fields are not generally thread-safe
* it is wrong for a class to have a public static final array field, or an accessor that returns such a field

### In public classes, use accessor methods, not public fields

* if a class is accessible outside its package, provide accessor methods
* if a class is package-private or is a private nested class, there is nothing inherently wrong with exposing its data fields

```java
// Encapsulation of data by accessor methods and mutators
class Point {
    private double x;
    private double y;

    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double getX() {
        return x;
    }

    public double getY() {
        return y;
    }

    public void setX(double x) {
        this.x = x;
    }

    public void setY(double y) {
        this.y = y;
    }
}
```

### Minimize mutability

An immutable class is simply a class whose instances cannot be modified. All of the information contained in each instance is fixed for the lifetime of the object, so no changes can ever be observed.



To make a class immutable, follow these five rules:

1. Don’t provide methods that modify the object’s state
2. Ensure that the class can’t be extended. Preventing subclassing is generally accomplished by making the class final, but there is an alternative. you can make all of its constructors private or package-private and add public static factories in place of the public constructors (Item 1)
3. Make all fields final
4. Make all fields private.
5. Ensure exclusive access to any mutable components. If your class has any fields that refer to mutable objects, ensure that clients of the class cannot obtain references to these objects. Never initialize such a field to a client-provided object reference or return the field from an accessor. Make defensive copies (Item 50) in constructors, accessors, and readObject methods (Item 88).
6. Immutable objects are simple. An immutable object can be in exactly one state, the state in which it was created.
7. Immutable objects are inherently thread-safe; they require no synchronization.
8. Since no thread can ever observe any effect of another thread on an immutable object, immutable objects can be shared freely.
9. Immutable objects make great building blocks for other objects,
10. Immutable objects provide failure atomicity for free (Item 76). Their state never changes, so there is no possibility of a temporary inconsistency.
11. Classes should be immutable unless there’s a very good reason to make them mutable.

The major disadvantage of immutable classes is that they require a separate object for each distinct value. Creating these objects can be costly, especially if they are large.

The performance problem is magnified if you perform a multistep operation that generates a new object at every step, eventually discarding all objects except the final result. There are two approaches to coping with this problem.&#x20;

The first is to guess which multistep operations will be commonly required and to provide them as primitives

mutable companion class. The main example of this approach in the Java platform libraries is the String class, whose mutable companion is StringBuilder (and its obsolete predecessor, StringBuffer)

### Favor composition over inheritance

* Unlike method invocation, inheritance violates encapsulation

```java
// Broken - Inappropriate use of inheritance!
public class InstrumentedHashSet<E> extends HashSet<E> {
    // The number of attempted element insertions
    private int addCount = 0;

    public InstrumentedHashSet() {
    }

    public InstrumentedHashSet(int initCap, float loadFactor) {
        super(initCap, loadFactor);
    }

    @Override
    public boolean add(E e) {
        addCount++;
        return super.add(e);
    }

    @Override
    public boolean addAll(Collection<? extends E> c) {
        addCount += c.size();
        return super.addAll(c);
    }

    public int getAddCount() {
        return addCount;
    }
}

InstrumentedHashSet<String> s = new InstrumentedHashSet<>();
s.addAll(List.of("Snap", "Crackle", "Pop"));
// with this addCount will be 6 instead of 3 as
// super.addAll() will call add which leads to double counting
```

### Design and document for inheritance or else prohibit it

the class must document its self-use of overridable methods.

a class may have to provide hooks into its internal workings in the form of judiciously chosen protected methods

The only way to test a class designed for inheritance is to write subclasses.

Therefore, you must test your class by writing subclasses before you release it.

Constructors must not invoke overridable methods, If the overriding method depends on any initialization performed by the subclass constructor, the method will not behave as expected.

because the clone and readObject methods behave a lot like constructors, a similar restriction applies: neither clone nor readObject may invoke an overridable method, directly or indirectly

### Prefer interfaces to abstract classes

Existing classes can easily be retrofitted to implement a new interface.

Interfaces are ideal for defining mixins. Loosely speaking, a mixin is a type that a class can implement in addition to its “primary type,” to declare that it provides some optional behavior

iterfaces enable safe, powerful functionality enhancements via the wrapper class idiom (Item 18). If you use abstract classes to define types, you leave the programmer who wants to add functionality with no alternative but inheritance. The resulting classes are less powerful and more fragile than wrapper classes

combine the advantages of interfaces and abstract classes by providing an abstract skeletal implementation class to go with an interface. The interface defines the type, perhaps providing some default methods, while the skeletal implementation class implements the remaining non-primitive interface methods atop the primitive interface methods. Extending a skeletal implementation takes most of the work out of implementing an interface. This is the Template Method pattern \[Gamma95

{% hint style="info" %}
By convention, skeletal implementation classes are called AbstractInterface, where Interface is the name of the interface they implement. For example, the Collections Framework provides a skeletal implementation to go along with each main collection interface: AbstractCollection, AbstractSet
{% endhint %}

.When properly designed, skeletal implementations (whether a separate abstract class, or consisting solely of default methods on an interface) can make it very easy for programmers to provide their own implementations of an interface. For example, here’s a static factory method containing a complete, fully functional List implementation atop AbstractList:

```java
static List<Integer> intArrayAsList(int[] a) {
        Objects.requireNonNull(a);
        // The diamond operator is only legal here in Java 9 and later
        // If you're using an earlier release, specify <Integer>
        return new AbstractList<>() {
            @Override
            public Integer get(int i) {
                return a[i]; // Autoboxing (Item 6)
            }

            @Override
            public Integer set(int i, Integer val) {
                int oldVal = a[i];
                a[i] = val; // Auto-unboxing
                return oldVal; // Autoboxing
            }

            @Override
            public int size() {
                return a.length;
            }
        };
    }
```

### Design interfaces for posterity

Prior to Java 8, it was impossible to add methods to interfaces without breaking existing implementations. If you added a new method to an interface, existing implementations would, in general, lack the method, resulting in a compile-time error. In Java 8, the default method construct was added \[JLS 9.4], with the intent of allowing the addition of methods to existing interfaces. But adding new methods to existing interfaces is fraught with risk.

it is not always possible to write a default method that maintains all invariants of every conceivable implementation.

In the presence of default methods, existing implementations of an interface may compile without error or warning but fail at runtime

it is still of the utmost importance to design interfaces with great care.

While it may be possible to correct some interface flaws after an interface is released, you cannot count on it

### Use interfaces only to define types

When a class implements an interface, the interface serves as a type that can be used to refer to instances of the class. That a class implements an interface should therefore say something about what a client can do with instances of the class. It is inappropriate to define an interface for any other purpose.

```java
// Some code// Constant interface antipattern - do not use!
public interface PhysicalConstants {
    // Avogadro's number (1/mol)
    static final double AVOGADROS_NUMBER = 6.022_140_857e23;
    // Boltzmann constant (J/K)
    static final double BOLTZMANN_CONSTANT = 1.380_648_52e-23;
    // Mass of the electron (kg)
    static final double ELECTRON_MASS = 9.109_383_56e-31;
}
```

The constant interface pattern is a poor use of interfaces. That a class uses some constants internally is an implementation detail. Implementing a constant interface causes this implementation detail to leak into the class’s exported API

### Prefer class hierarchies to tagged classes

```java
// Tagged class - vastly inferior to a class hierarchy!
class Figure {
    enum Shape {
        RECTANGLE, CIRCLE
    };

    // Tag field - the shape of this figure
    final Shape shape;
    // These fields are used only if shape is RECTANGLE
    double length;
    double width;
    // This field is used only if shape is CIRCLE
    double radius;

    // Constructor for circle
    Figure(double radius) {
        shape = Shape.CIRCLE;
        this.radius = radius;
    }

    // Constructor for rectangle
    Figure(double length, double width) {
        shape = Shape.RECTANGLE;
        this.length = length;
        this.width = width;
    }

    double area() {
        switch (shape) {
            case RECTANGLE:
                return length * width;
            case CIRCLE:
                return Math.PI * (radius * radius);
            default:
                throw new AssertionError(shape);
        }
    }
}
```

tagged classes are verbose, error-prone, and inefficient

A tagged class is just a pallid imitation of a class hierarchy

```java
// Class hierarchy replacement for a tagged class
abstract class Figure {
    abstract double area();
}

class Circle extends Figure {
    final double radius;
    Circle(double radius) { this.radius = radius; }
    @Override double area() { return Math.PI * (radius * radius); }
    }
    class Rectangle extends Figure {
    final double length;
    final double width;
    Rectangle(double length, double width) {
    this.length = length;
    this.width = width;
    }
    @Override double area() { return length * width; }
    }
```

### Favor static member classes over nonstatic

A nested class is a class defined within another class. A nested class should exist only to serve its enclosing class. If a nested class would be useful in some other context, then it should be a top-level class. There are four kinds of nested classes: static member classes, nonstatic member classes, anonymous classes, and local classes. All but the first kind are known as inner classes.

Each instance of a nonstatic member class is implicitly associated with an enclosing instance of its containing class. Within instance methods of a nonstatic member class, you can invoke methods on the enclosing instance or obtain a reference to the enclosing instance using the qualified this construct \[JLS, 15.8.4]. If an instance of a nested class can exist in isolation from an instance of its enclosing class, then the nested class must be a static member class: it is impossible to create an instance of a nonstatic member class without an enclosing instance

If you declare a member class that does not require access to an enclosing instance, always put the static modifier in its declaration, making it a static rather than a nonstatic member class. If you omit this modifier, each instance will have a hidden extraneous reference to its enclosing instance. As previously mentioned, storing this reference takes time and space. More seriously, it can result in the enclosing instance being retained when it would otherwise be eligible for garbage collection (Item 7). The resulting memory leak can be catastrophic. It is often difficult to detect because the reference is invisible.

### Limit source files to a single top-level class

While the Java compiler lets you define multiple top-level classes in a single source file, there are no benefits associated with doing so, and there are significant risks. The risks stem from the fact that defining multiple top-level classes in a source file makes it possible to provide multiple definitions for a class. Which definition gets used is affected by the order in which the source files are passed to the compiler

as an alternative to splitting the classes into separate source files. If the classes are subservient to another class, making them into static member classes is generally the better alternative because it enhances readability and makes it possible to reduce the accessibility of the classes by declaring them private
