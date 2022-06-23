---
description: >-
  The Java Iterable interface represents a collection of objects which is
  iterable - meaning which can be iterated.
---

# Java Iterable

### Iterate an Iterable With the for-each Loop

The first way to iterate the elements of a Java Iterable is via the [Java for-each loop](https://jenkov.com/java/for.html#the-java-for-each-loop) loop.



```java
List<String> list = new ArrayList><();

list.add("one");
list.add("two");
list.add("three");

for( String element : list ){
    System.out.println( element.toString() );
}a
```

### Iterate an Iterable via an Iterator

The second way you can iterate the elements of a Java Iterable is by obtaining a Java Iterator from it by calling the Iterable `iterator()` method. You can then iterate through that Iterator like you would with any other Iterator



```java
List<String> list = new ArrayList><();

list.add("one");
list.add("two");
list.add("three");

Iterator<String> iterator = list.iterator();

while(iterator.hasNext()) {
    String element = iterator.next();
    System.out.println( element );
}va
```

### Iterate an Iterable via its forEach() Method

The third way to iterate the elements of a Java Iterable is via its `forEach()` method. The `forEach()` method takes a [Java Lambda Expression](https://jenkov.com/java/lambda-expressions.html) as parameter.



```java
List<String> list = new ArrayList><();

list.add("one");
list.add("two");
list.add("three");

list.forEach( (element) -> {
    System.out.println( element );
});
```



### Iterable Interface Definition

The Java `Iterable` interface has three methods of which only one needs to be implemented. The other two have default implementations. Here is the the definition of the Iterable interface:

```java
public interface Iterable<T> {

  Iterator<T>    iterator();

  Spliterator<T> spliterator();

  void           forEach(Consumer<? super T> action);

}
```

### Iterable Performance

If you are writing some code that needs to iterate a collection lots of times in a tight loop, let's say iterate a [Java List](https://jenkov.com/tutorials/java-collections/list.html) thousands of times per second, iterating the `List` via the Java for-each loop is slower than iterating the list via a standard for-loop as seen here: () .

```java
for(int i=0; i<list.size(); i++) {
    Object obj = list.get(i);
}
```

The reason the for-each loop is slower is, that each iteration will call the `List` `iterator()` method, which will create a new `Iterator` object.
