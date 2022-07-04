# Java Set

The _Java_ _Set_ interface, `java.util.Set`, represents a collection of objects where each object in the Java _Set_ is unique. In other words, the same object cannot occur more than once in a Java _Set_.



Since `Set` is an interface you need to instantiate a concrete implementation of the interface in order to use it. You can choose between the following `Set` implementations in the Java Collections API:

* java.util.EnumSet
* java.util.HashSet: `HashSet` is backed by a `HashMap`. It makes no guarantees about the sequence of the elements when you iterate them.
* java.util.LinkedHashSet: guarantees the order of the elements during iteration is the same as the order they were inserted into the `LinkedHashSet`. Reinserting an element that is already in the `LinkedHashSet` does not change this order
* java.util.TreeSet: `TreeSet` also guarantees the order of the elements when iterated, but the order is the sorting order of the elements.

### Set.of()



The Java Set static factory methods are called `of()` and take either zero or more parameters. Here is first an example of creating an empty, immutable Set using `Set.of()` :

```java
Set set = Set.of();

// Specify Generic Type
Set<String> set3 = Set.<String>of("val1", "val2", "val3");
```

### Iterate Set Using the Java Stream API



```java
Stream<String> stream = set.stream();

stream.forEach((element) ->         { System.out.println(element); });
```

### Convert Java Set to List



```java
Set<String> set = new HashSet<>();
set.add("123");
set.add("456");

List<String> list = new ArrayList<>();
list.addAll(set);
```
