# Creating and Destroying Objects

### Consider static factory methods instead of constructors

#### &#x20;A static factory with a well-chosen name is easier to use and the resulting client code easier to read than constructors

Example: BigInteger(int, int, Random), which returns a BigInteger that is probably prime, would have been better expressed as a static factory method named BigInteger.probablePrime.

#### This allows immutable classes to use preconstructed instances, or to cache instances as they’re constructed, and dispense them repeatedly to avoid creating unnecessary duplicate objects.

Example: The Boolean.valueOf(boolean) method illustrates this technique: it never creates an object. This technique is similar to the Flyweight pattern \[Gamma95]



#### Unlike constructors, they can return an object of any subtype of their return type. This gives you great flexibility in choosing the class of the returned object. This technique lends itself to interface-based frameworks (Item 20), where interfaces provide natural return types for static factory methods.

Example: . For example, the Java Collections Framework has forty-five utility implementations of its interfaces, providing unmodifiable collections, synchronized collections, and the like. Nearly all of these implementations are exported via static factory methods in one noninstantiable class (java.util.Collections). The classes of the returned objects are all nonpublic.

#### The class of the returned object can vary from call to call as a function of the input parameters. Any subtype of the declared return type is permissible. The class of the returned object can also vary from release to release.

Example: The EnumSet class (Item 36) has no public constructors, only static factories. In the OpenJDK implementation, they return an instance of one of two subclasses, depending on the size of the underlying enum type: if it has sixty-four or fewer elements, as most enum types do, the static factories return a RegularEnumSet instance, which is backed by a single long; if the enum type has sixty-five or more elements, the factories return a JumboEnumSet instance, backed by a long array.

#### The class of the returned object need not exist when the class containing the method is written.

Example: Such flexible static factory methods form the basis of service provider frameworks, like the Java Database Connectivity API (JDBC). A service provider framework is a system in which providers implement a service, and the system makes the implementations available to clients, decoupling the clients from the implementations

#### Limitations

* The main limitation of providing only static factory methods is that classes without public or protected constructors cannot be subclassed.
* A second shortcoming of static factory methods is that they are hard for programmers to find. Document them better

#### Comman static factory methods

• from—A type-conversion method that takes a single parameter and returns a corresponding instance of this type, for example: Date d = Date.from(instant); • of—An aggregation method that takes multiple parameters and returns an instance of this type that incorporates them, for example: Set faceCards = EnumSet.of(JACK, QUEEN, KING);&#x20;

• valueOf—A more verbose alternative to from and of, for example: BigInteger prime = BigInteger.valueOf(Integer.MAX\_VALUE);&#x20;

• instance or getInstance—Returns an instance that is described by its parameters (if any) but cannot be said to have the same value, for example: StackWalker luke = StackWalker.getInstance(options);&#x20;

• create or newInstance—Like instance or getInstance, except that the method guarantees that each call returns a new instance, for example: Object newArray = Array.newInstance(classObject, arrayLen);&#x20;

• getType—Like getInstance, but used if the factory method is in a different class. Type is the type of object returned by the factory method, for example: FileStore fs = Files.getFileStore(path);&#x20;

• newType—Like newInstance, but used if the factory method is in a different class. Type is the type of object returned by the factory method, for example: BufferedReader br = Files.newBufferedReader(path);&#x20;

• type—A concise alternative to getType and newType, for example: List litany = Collections.list(legacyLitany);

### Consider a builder when faced with many constructor parameters

Static factories and constructors share a limitation: they do not scale well to large numbers of optional parameters.

#### Alternative 1: telescoping constructor pattern

provide a constructor with only the required parameters, another with a single optional parameter, a third with two optional parameters, and so on, culminating in a constructor with all the optional parameters.

```java
// Telescoping constructor pattern - does not scale well!
public class NutritionFacts {
private final int servingSize; // (mL) required
private final int servings; // (per container) required
private final int calories; // (per serving) optional
private final int fat; // (g/serving) optional
private final int sodium; // (mg/serving) optional
private final int carbohydrate; // (g/serving) optional

public NutritionFacts(int servingSize, int servings) {
this(servingSize, servings, 0);
}

public NutritionFacts(int servingSize, int servings,
int calories) {
this(servingSize, servings, calories, 0);
}

public NutritionFacts(int servingSize, int servings,
int calories, int fat) {
this(servingSize, servings, calories, fat, 0);
}

public NutritionFacts(int servingSize, int servings,
int calories, int fat, int sodium) {
this(servingSize, servings, calories, fat, sodium, 0);
}

public NutritionFacts(int servingSize, int servings,
int calories, int fat, int sodium, int carbohydrate) {
this.servingSize = servingSize;
this.servings = servings;
this.calories = calories;
this.fat = fat;
this.sodium = sodium;
this.carbohydrate = carbohydrate;
}
}

```

{% hint style="warning" %}
the telescoping constructor pattern works, but it is hard to write client code when there are many parameters, and harder still to read it
{% endhint %}

#### Alternative 2: JavaBeans Pattern

in which you call a parameterless constructor to create the object and then call setter methods to set each required parameter and each optional parameter of interest

```java
// JavaBeans Pattern - allows inconsistency, mandates mutability
public class NutritionFacts {
// Parameters initialized to default values (if any)
private int servingSize = -1; // Required; no default value
private int servings = -1; // Required; no default value
private int calories = 0;
private int fat = 0;
private int sodium = 0;
private int carbohydrate = 0;

// empty constructors
public NutritionFacts() { }

// Setters
public void setServingSize(int val) { servingSize = val; }
public void setServings(int val) { servings = val; }
public void setCalories(int val) { calories = val; }
public void setFat(int val) { fat = val; }
public void setSodium(int val) { sodium = val; }
public void setCarbohydrate(int val) { carbohydrate = val; }
}

// instantiate
NutritionFacts cocaCola = new NutritionFacts();
cocaCola.setServingSize(240);
cocaCola.setServings(8);
cocaCola.setCalories(100);
cocaCola.setSodium(35);
cocaCola.setCarbohydrate(27);
```

{% hint style="warning" %}
Because construction is split across multiple calls, a JavaBean may be in an inconsistent state partway through its construction. The class does not have the option of enforcing consistency merely by checking the validity of the constructor parameters

It is possible to reduce these disadvantages by manually “freezing” the object when its construction is complete and not allowing it to be used until frozen, but this variant is unwieldy and rarely used in practice. Moreover, it can cause errors at runtime because the compiler cannot ensure that the programmer calls the freeze method on an object before using i
{% endhint %}

#### Alternative 3: Builder pattern

Instead of making the desired object directly, the client calls a constructor (or static factory) with all of the required parameters and gets a builder object. Then the client calls setter-like methods on the builder object to set each optional parameter of interest. Finally, the client calls a parameterless build method to generate the object, which is typically immutable. The builder is typically a static member class (Item 24) of the class it builds.

```java
// Builder Pattern
public class NutritionFacts {
private final int servingSize;
private final int servings;
private final int calories;
private final int fat;
private final int sodium;
private final int carbohydrate;

    public static class Builder {
    // Required parameters
    private final int servingSize;
    private final int servings;
    // Optional parameters - initialized to default values
    private int calories = 0;
    private int fat = 0;
    private int sodium = 0;
    private int carbohydrate = 0;

    public Builder(int servingSize, int servings) {
    this.servingSize = servingSize;
    this.servings = servings;
    }

    public Builder calories(int val)
    { calories = val; return this; }
    public Builder fat(int val)
    { fat = val; return this; }
    public Builder sodium(int val)
    { sodium = val; return this; }
    public Builder carbohydrate(int val)
    { carbohydrate = val; return this; }
    public NutritionFacts build() {
    return new NutritionFacts(this);
    }
    }

    private NutritionFacts(Builder builder) {
    servingSize = builder.servingSize;
    servings = builder.servings;
    calories = builder.calories;
    fat = builder.fat;
    sodium = builder.sodium;
    carbohydrate = builder.carbohydrate;
    }
}

// instantiate 
NutritionFacts cocaCola = new NutritionFacts.Builder(240, 8)
.calories(100).sodium(35).carbohydrate(27).build();

```

{% hint style="info" %}
The Builder pattern simulates named optional parameters as found in Python and Scala.
{% endhint %}

```java
// Builder pattern for class hierarchies
public abstract class Pizza {
    public enum Topping { HAM, MUSHROOM, ONION, PEPPER, SAUSAGE }
    final Set<Topping> toppings;

    abstract static class Builder<T extends Builder<T>> {
        EnumSet<Topping> toppings = EnumSet.noneOf(Topping.class);
        
        public T addTopping(Topping topping) {
        toppings.add(Objects.requireNonNull(topping));
        return self();
        }

        abstract Pizza build();

        // Subclasses must override this method to return "this"
        protected abstract T self();
    }

    Pizza(Builder<?> builder) {
        toppings = builder.toppings.clone(); // See Item 50
    }
}

public class NyPizza extends Pizza {
    public enum Size { SMALL, MEDIUM, LARGE }
    private final Size size;

    public static class Builder extends Pizza.Builder<Builder> {
        private final Size size;
        
        public Builder(Size size) {
            this.size = Objects.requireNonNull(size);
        }
        
        @Override public NyPizza build() {
            return new NyPizza(this);
        }
        
        @Override protected Builder self() { return this; }
    }
    
    private NyPizza(Builder builder) {
        super(builder);
        size = builder.size;
    }
}

NyPizza pizza = new NyPizza.Builder(SMALL)
.addTopping(SAUSAGE).addTopping(ONION).build();
```

{% hint style="warning" %}
The Builder pattern has disadvantages as well. In order to create an object, you must first create its builder. While the cost of creating this builder is unlikely to be noticeable in practice, it could be a problem in performance-critical situations. Also, the Builder pattern is more verbose than the telescoping constructor pattern, so it should be used only if there are enough parameters to make it worthwhile, say four or more.
{% endhint %}

### Enforce the singleton property with a private constructor or an enum type&#x20;

A singleton is simply a class that is instantiated exactly once \[Gamma95]. Singletons typically represent either a stateless object such as a function (Item 24) or a system component that is intrinsically unique. Making a class a singleton can make it difficult to test its clients because it’s impossible to substitute a mock implementation for a singleton unless it implements an interface that serves as its type

#### Two ways to implement

```
// Singleton with public final field
public class Elvis {
public static final Elvis INSTANCE = new Elvis();
private Elvis() { ... }
public void leaveTheBuilding() { ... }
}

// Singleton with static factory
public class Elvis {
private static final Elvis INSTANCE = new Elvis();
private Elvis() { ... }
public static Elvis getInstance() { return INSTANCE; }
public void leaveTheBuilding() { ... }
}
```

The main advantage of the public field approach is that the API makes it clear that the class is a singleton: the public static field is final, so it will always contain the same object reference. The second advantage is that it’s simpler.&#x20;

One advantage of the static factory approach is that it gives you the flexibility to change your mind about whether the class is a singleton without changing its API. The factory method returns the sole instance, but it could be modified to return, say, a separate instance for each thread that invokes it. A second advantage is that you can write a generic singleton factory if your application requires it (Item 30). A final advantage of using a static factory is that a method reference can be used as a supplier, for example Elvis::instance is a Supplier. Unless one of these advantages is relevant, the public field approach is preferable

{% hint style="warning" %}
To make a singleton class that uses either of these approaches serializable (Chapter 12), it is not sufficient merely to add implements Serializable to its declaration. To maintain the singleton guarantee, declare all instance fields transient and provide a readResolve method
{% endhint %}

```java
// readResolve method to preserve singleton property
private Object readResolve() {
// Return the one true Elvis and let the garbage collector
// take care of the Elvis impersonator.
return INSTANCE;
}
```

#### Third and preferred way

```java
// Enum singleton - the preferred approach
public enum Elvis {
INSTANCE;
public void leaveTheBuilding() { ... }
}

```

This approach is similar to the public field approach, but it is more concise, provides the serialization machinery for free, and provides an ironclad guarantee against multiple instantiation,

A single-element enum type is often the best way to implement a singleton. Note that you can’t use this approach if your singleton must extend a superclass other than Enum (though you can declare an enum to implement interfaces).

### Enforce noninstantiability with a private constructor

A default constructor is generated only if a class contains no explicit constructors, so a class can be made noninstantiable by including a private constructor

```java
// Noninstantiable utility class
public class UtilityClass {
// Suppress default constructor for noninstantiability
private UtilityClass() {
throw new AssertionError();
}
... // Remainder omitted
}
```

### Prefer dependency injection to hardwiring resources

A simple pattern that satisfies this requirement is to pass the resource into the constructor when creating a new instance.

```java
// Dependency injection provides flexibility and testability
public class SpellChecker {
private final Lexicon dictionary;
public SpellChecker(Lexicon dictionary) {
this.dictionary = Objects.requireNonNull(dictionary);
}
public boolean isValid(String word) { ... }
public List<String> suggestions(String typo) { ... }
}
```

A useful variant of the pattern is to pass a resource factory to the constructor. The Supplier interface, introduced in Java 8, is perfect for representing factories. Methods that take a Supplier on input should typically constrain the factory’s type parameter using a bounded wildcard type (Item 31) to allow the client to pass in a factory that creates any subtype of a specified type.

For example, here is a method that makes a mosaic using a client-provided factory to produce each tile:

```java
Mosaic create(Supplier<? extends Tile> tileFactory) { ... }
```

### Avoid creating unnecessary objects

t is often appropriate to reuse a single object instead of creating a new functionally equivalent object each time it is needed. Reuse can be both faster and more stylish. An object can always be reused if it is immutable

Example

```java
// Example 1
String s = new String("bikini"); // DON'T DO THIS!
String s = "bikini"; // DO THIS. IT RESUSES

// Example 2
// Performance can be greatly improved!
static boolean isRomanNumeral(String s) {
    return s.matches("^(?=.)M*(C[MD]|D?C{0,3})"
        + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");
}
// Compile once and cache it, keep using cached 
private static final Pattern ROMAN = Pattern.compile(
        "^(?=.)M*(C[MD]|D?C{0,3})"
            + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");
static boolean isRomanNumeral(String s) {
    return ROMAN.matcher(s).matches();
}

// Example 3
// Hideously slow! Can you spot the object creation?
private static long sum() {
Long sum = 0L; // Long is object type and slow, use long instead 
for (long i = 0; i <= Integer.MAX_VALUE; i++)
sum += i;
return sum;
}
```

{% hint style="info" %}
prefer primitives to boxed primitives, and watch out for unintentional autoboxing.
{% endhint %}

{% hint style="warning" %}
avoiding object creation by maintaining your own object pool is a bad idea unless the objects in the pool are extremely heavyweight. The classic example of an object that does justify an object pool is a database connection
{% endhint %}

### Eliminate obsolete object references&#x20;

If an object reference is unintentionally retained, not only is that object excluded from garbage collection, but so too are any objects referenced by that object, and so on

```java
// Can you spot the "memory leak"?
public class Stack {
private Object[] elements;
private int size = 0;
private static final int DEFAULT_INITIAL_CAPACITY = 16;

public Stack() {
elements = new Object[DEFAULT_INITIAL_CAPACITY];
}

public void push(Object e) {
ensureCapacity();
elements[size++] = e;
}

public Object pop() {
if (size == 0)
throw new EmptyStackException();
return elements[--size]; // MEMORY LEAK
}

public Object popFixedMemoryLeak() {
if (size == 0)
throw new EmptyStackException();
Object result = elements[--size];
elements[size] = null; // Eliminate obsolete reference
return result;
}

/**
* Ensure space for at least one more element, roughly
* doubling the capacity each time the array needs to grow.
*/
private void ensureCapacity() {
if (elements.length == size)
elements = Arrays.copyOf(elements, 2 * size + 1);
}
}
```

{% hint style="warning" %}
whenever a class manages its own memory, the programmer should be alert for memory leaks. Whenever an element is freed, any object references contained in the element should be nulled out
{% endhint %}

Other Examples: Caches, listeners and other callbacks

### Avoid finalizers and cleaners

One shortcoming of finalizers and cleaners is that there is no guarantee they’ll be executed promptly

It can take arbitrarily long between the time that an object becomes unreachable and the time its finalizer or cleaner runs. This means that you should never do anything time-critical in a finalizer or cleaner.

The promptness with which finalizers and cleaners are executed is primarily a function of the garbage collection algorithm, which varies widely across implementations

you should never depend on a finalizer or cleaner to update persistent state. For example, depending on a finalizer or cleaner to release a persistent lock on a shared resource such as a database is a good way to bring your entire distributed system to a grinding halt.

There is a severe performance penalty for using finalizers and cleaners

Finalizers have a serious security problem: they open your class up to finalizer attacks.

Throwing an exception from a constructor should be sufficient to prevent an object from coming into existence; in the presence of finalizers, it is not.

{% hint style="info" %}
To protect nonfinal classes from finalizer attacks, write a final finalize method that does nothing.
{% endhint %}

. So what should you do for a class whose objects encapsulate resources that require termination, such as files or threads? Just have your class implement AutoCloseable, and require its clients to invoke the close method on each instance when it is no longer needed, typically using try-with-resources to ensure termination even in the face of exceptions (Item 9). One detail worth mentioning is that the instance must keep track of whether it has been closed: the close method must record in a field that the object is no longer valid, and other methods must check this field and throw an IllegalStateException if they are called after the object has been closed.

#### So what, if anything, are cleaners and finalizers good for

One is to act as a safety net in case the owner of a resource neglects to call its close method. While there’s no guarantee that the cleaner or finalizer will run promptly (or at all), it is better to free the resource late than never if the client fails to do so. Ex: FileOutputStream, ThreadPoolExecutor

A second legitimate use of cleaners concerns objects with native peers. A native peer is a native (non-Java) object to which a normal object delegates via native methods. Because a native peer is not a normal object, the garbage collector doesn’t know about it and can’t reclaim it when its Java peer is reclaimed

```java
// An autocloseable class using a cleaner as a safety net
public class Room implements AutoCloseable {
private static final Cleaner cleaner = Cleaner.create();

// Resource that requires cleaning. Must not refer to Room!(will 
// cause circular dependency))
private static class State implements Runnable {
int numJunkPiles; // Number of junk piles in this room
State(int numJunkPiles) {
this.numJunkPiles = numJunkPiles;
}

// Invoked by close method or cleaner
// no guarantee to run as cleaners are implementation specific
@Override public void run() {
System.out.println("Cleaning room");
numJunkPiles = 0;
}
}
// The state of this room, shared with our cleanable
private final State state;
// Our cleanable. Cleans the room when it’s eligible for gc
private final Cleaner.Cleanable cleanable;
public Room(int numJunkPiles) {
state = new State(numJunkPiles);
cleanable = cleaner.register(this, state);
}
@Override public void close() {
cleanable.clean();
}
}
```

#### Try with resource over try finally

```java
// try-finally - No longer the best way to close resources!
static String firstLineOfFile(String path) throws IOException {
BufferedReader br = new BufferedReader(new FileReader(path));
try {
    return br.readLine();
} finally {
    br.close();
}
}

// try-with-resources - the the best way to close resources!
static String firstLineOfFile(String path) throws IOException {
try (BufferedReader br = new BufferedReader(
new FileReader(path))) {
return br.readLine();
}
}
```

```java
// try-finally is ugly when used with more than one resource!
static void copy(String src, String dst) throws IOException {
    InputStream in = new FileInputStream(src);
    try {
        OutputStream out = new FileOutputStream(dst);
        try {
            byte[] buf = new byte[BUFFER_SIZE];
            int n;
            while ((n = in.read(buf)) >= 0)
            out.write(buf, 0, n);
        } finally {
        out.close();
        }
    } finally {
    in.close();
    }
}

// try-with-resources on multiple resources - short and sweet
static void copy(String src, String dst) throws IOException {
    try (InputStream in = new FileInputStream(src);
    OutputStream out = new FileOutputStream(dst)) {
    byte[] buf = new byte[BUFFER_SIZE];
    int n;
    while ((n = in.read(buf)) >= 0)
    out.write(buf, 0, n);
    }
}
```
