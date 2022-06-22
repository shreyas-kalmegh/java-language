# Generics

### **The Need for Generics**

```java
List list = new LinkedList();
list.add(new Integer(1)); 
Integer i = list.iterator().next(); // compile error
// Object returned by iterator needs to be casted

Integer i = (Integer) list.iterator.next();
```

```java
List<Integer> list = new LinkedList<Integer>();
List<Integer> list = new LinkedList<>();
// both will work
```

By adding the diamond operator <> containing the type, we narrow the specialization of this list to only _Integer_ type

### **Generic Methods**

We write generic methods with a single method declaration, and we can call them with arguments of different types. The compiler will ensure the correctness of whichever type we use.



These are some properties of generic methods:

* Generic methods have a type parameter (the diamond operator enclosing the type) before the return type of the method declaration.
* Type parameters can be bounded (we explain bounds later in this article).
* Generic methods can have different type parameters separated by commas in the method signature.
* Method body for a generic method is just like a normal method.



```java
// Generic function definition
public <T> List<T> fromArrayToList(T[] a) {   
    return Arrays.stream(a).collect(Collectors.toList());
}
```

{% hint style="info" %}
The _\<T>_ in the method signature implies that the method will be dealing with generic type _T_. This is needed even if the method is returning void.
{% endhint %}

```java
// Generic functions dealing with two types: T and G
public static <T, G> List<G> fromArrayToList(T[] a, Function<T, G> mapperFunction) {
    return Arrays.stream(a)
      .map(mapperFunction)
      .collect(Collectors.toList());
}
```

### **Bounded Generics**

we can specify that a method accepts a type and all its sub-classes (upper bound) or a type and all its superclasses (lower bound).



To declare an upper-bounded type, we use the keyword _extends_ after the type, followed by the upper bound that we want to use:

```java
public <T extends Number> List<T> fromArrayToList(T[] a) {
    ...
}
```

### **Multiple Bounds**

A type can also have multiple upper bounds:

```java
<T extends Number & Comparable>
```

{% hint style="warning" %}
If one of the types that are extended by _T_ is a class (e.g. _Number_), we have to put it first in the list of bounds. Otherwise, it will cause a compile-time error.
{% endhint %}

### **Using Wildcards With Generics**

Wildcards are represented by the question mark _?_ in Java, and we use them to refer to an unknown type.



```java
public static void paintAllBuildings(List<Building> buildings) {
    buildings.forEach(Building::paint);
}

// will not work with List<House>, where House is a sub-class of Building

// Use  wildcard to support this behaviour
public static void paintAllBuildings(List<? extends Building> buildings) {
    ...
}

```

_\<? extends T>_ means unknown type that is a sub-class of _T( used for upper bound wildcard)_

_\<? super T>_ means unknown type that is a super-class of _T( used for lower bound wildcard)_

### **Type Erasure**

Generics were added to Java to ensure type safety. And to ensure that generics won't cause overhead at runtime, the compiler applies a process called _type erasure_ on generics at compile time.

Type erasure removes all type parameters and replaces them with their bounds or with _Object_ if the type parameter is unbounded. This way, the bytecode after compilation contains only normal classes, interfaces and methods, ensuring that no new types are produced. Proper casting is applied as well to the _Object_ type at compile time.



This is an example of type erasure:

```java
public <T> List<T> genericMethod(List<T> list) {
    return list.stream().collect(Collectors.toList());
}
```

With type erasure, the unbounded type _T_ is replaced with _Object_:

```java
// for illustration
public List<Object> withErasure(List<Object> list) {
    return list.stream().collect(Collectors.toList());
}

// which in practice results in
public List withErasure(List list) {
    return list.stream().collect(Collectors.toList());
}
```

### **Generics and Primitive Data Types**

{% hint style="info" %}
One restriction of generics in Java is that the type parameter cannot be a primitive type
{% endhint %}

To understand why primitive data types don't work, let's remember that **generics are a compile-time feature**, meaning the type parameter is erased and all generic types are implemented as type _Object_.



```java
List<int> list = new ArrayList<>(); // will not compile
list.add(17);

List<Integer> list = new ArrayList<>(); // will compile
list.add(17);
```
