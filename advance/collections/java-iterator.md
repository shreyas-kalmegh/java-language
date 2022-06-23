---
description: >-
  The Java Iterator interface represents an object capable of iterating through
  a collection of Java objects, one object at a time
---

# Java Iterator

The Java Iterator interface is reasonably simple. The core methods of the Iterator interface are:

| Method             | Description                                                                                                                                                                                                      |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| hasNext()          | Returns `true` if the Iterator has more elements, and `false` if not.                                                                                                                                            |
| next()             | Return the next element from the Iterator                                                                                                                                                                        |
| remove()           | Removes the latest element returned from next() from the Collection the Iterator is iterating over.                                                                                                              |
| forEachRemaining() | Iterates over all remaining elements in the Iterator and calls a [Java Lambda Expression](https://jenkov.com/java/lambda-expressions.html) passing each remaining element as parameter to the lambda expression. |

### Obtaining an Iterator

The standard Java collection interface `Collection` contains a method called `iterator()`. By calling `iterator()` you can obtain an iterator from the given `Collection`

```java
List<String> list = new ArrayList<>();
list.add("one");
list.add("two");
list.add("three");

Iterator<String> iterator = list.iterator();
```



### Iterating an Iterator

You iterate the objects in an `Iterator` using a `while` loop. Here is an example of iterating the elements of a Java `Iterator` using a while loop:

```
Iterator iterator = list.iterator();

while(iterator.hasNext()) {
    Object nextObject = iterator.next();

}
```

### Iteration Order

The order in which the elements contained in a Java `Iterator` are traversed depends on the object that supplies the `Iterator`. For instance, an iterator obtained from a `List` will iterate through the elements of that `List` in the same order the elements are stored internally in the `List`. An `Iterator` obtained from a `Set`, on the other hand, does not make any guarantees about the exact sequence the elements in the `Set` are iterated in.

### Modification During Iteration

Some collections do not allow you to modify the collection while you are iterating it via an `Iterator`. In that case you will get a `ConcurrentModificationException` the next time you call the `Iterator` `next()` method.

The `ConcurrentModificationException` is thrown because the `Iterator` gets out of sync with the collection, if you modify the collection while iterating it via the `Iterator`

### Remove Elements During Iteration

The Java `Iterator` interface has a `remove()` method which lets you remove the element just returned by `next()` from the underlying collection. Calling `remove()` does not cause a `ConcurrentModificationException` to be thrown.



### forEachRemaining()

The Java Iterator `forEachRemaining()` method can iterate over all of the elements remaining in the Iterator internally, and for each element call a [Java Lambda Expression](https://jenkov.com/java/lambda-expressions.html) passed as parameter to `forEachRemaining()`&#x20;

```java
List<String> list = new ArrayList<>();
list.add("Jane");
list.add("Heidi");
list.add("Hannah");

Iterator<String> iterator = list.iterator();
        
iterator.forEachRemaining((element) -> {
    System.out.println(element);
});
```

### ListIterator

Java also contains an interface called ListIterator which extends the Iterator interface. The Java ListIterator interface which represents a bi-directional iterator - meaning an iterator where you can navigate the elements both forward and backwards



```java
List<String> list = new ArrayList<>();
list.add("Jane");
list.add("Heidi");
list.add("Hannah");

ListIterator<String> listIterator = list.listIterator();
        
while(listIterator.hasNext()) {
    System.out.println(listIterator.next());
}
        
while(listIterator.hasPrevious()) {
    System.out.println(listIterator.previous());
}
```

### Implement the Iterator Interface in Your Own Class

If you have a special, custom made type of collection, you can implement the Java Iterator interface yourself to create an Iterator that can iterate through the elements of your custom collection



```java
import java.util.Iterator;
import java.util.List;

public class ListIterator <T> implements Iterator<T> {

    private List<T> source = null;
    private int index = 0;

    public ListIterator(List<T> source){
        this.source = source;
    }


    @Override
    public boolean hasNext() {
        return this.index < this.source.size();
    }

    @Override
    public T next() {
        return this.source.get(this.index++);
    }

}
```
