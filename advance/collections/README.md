---
description: >-
  The Java Collections API provide Java developers with a set of classes and
  interfaces that makes it easier to work with collections of objects, e.g.
  lists, maps, stacks etc.
---

# Collections



The core interfaces of the Java Collection API are:

* [Java Collection](https://jenkov.com/tutorials/java-collections/collection.html): The Java Collection interface represents the operations possible on a generic collection, like on a List, Set, Stack, Queue and Deque
* [Java List](https://jenkov.com/tutorials/java-collections/list.html): The Java List interface represents an ordered collection of objects. By ordered means, that you can access the elements in the order they occur in the list.
* [Java Set](https://jenkov.com/tutorials/java-collections/set.html): The Java Set interface represents an unordered collection of objects. Unlike the List, a Set does not allow you to access the elements of a Set in any guaranteed order. There are Set implementations that order elements based on their natural ordering, but the Set interface itself provides no such guarantees
* [Java SortedSet](https://jenkov.com/tutorials/java-collections/sortedset.html): The Java SortedSet interface represents an ordered collection of objects. Thus, the elements in the SortedSet can be iterated in the sorted order.
* [Java navigableSet](https://jenkov.com/tutorials/java-collections/navigableset.html): The Java NavigableSet interface is an extension of the SortedSet interface with additional methods for eay navigation of the elements in the NavigableSet
* [Java Map](https://jenkov.com/tutorials/java-collections/map.html): The Java Map interface represents a mapping between sets of keys and values. Both keys and values are objects. You insert a key + value pair into a Map, and later you can retrieve the value via the key - meaning you only need the key to read the value out of the Map again later.
* [Java SortedMap](https://jenkov.com/tutorials/java-collections/sortedmap.html): The Java SortedMap interface is an extension of the Map interface, representing a Map where the keys in the Map are sorted. Thus, you can iterate the keys stored in the SortedMap in the sorted order,
* [Java NavigableMap](https://jenkov.com/tutorials/java-collections/navigablemap.html): The Java NavigableMap interface is an extension of the SortedMap interface which contains additional methods for easy navigation of the keys and entries in the NavigableMap.
* [Java Stack](https://jenkov.com/tutorials/java-collections/stack.html): The Java Stack class represents a classical stack data structure, where elements can be pushed to the top of the stack, and popped off from the top of the stack again later.
* [Java Queue](https://jenkov.com/tutorials/java-collections/queue.html): The Java Queue interface represents a classical queue data structure, where objects are inserted into one end of the queue, and taken off the queue in the other end of the queue.
* [Java Deque](https://jenkov.com/tutorials/java-collections/deque.html): The Java Deque interface represents a double ended queue, meaning a data structure where you can insert and remove elements from both ends of the queue
* [Java Iterator](https://jenkov.com/tutorials/java-collections/iterator.html): The Java Iterator interface represents a component that is capable of iterating a Java collection of some kind. For instance, a List or a Set. You can obtain an Iterator instance from the Java Set, List, Map etc.
* [Java Iterable](https://jenkov.com/tutorials/java-collections/iterable.html): The Java Iterable interface is very similar in responsibility to the Java Iterator interface. The Iterable interface allows a Java Collection to be iterated using the for-each loop in Java



The Java Collections API also contains useful implementations of the above interfaces, and a few other utility classes. Some of these are:

* [Collections](https://jenkov.com/tutorials/java-collections/collections.html): The [Java Collections class](https://jenkov.com/tutorials/java-collections/collections.html) contains a range of utility methods that help you work more efficiently with the Java Collections API.
* [Properties](https://jenkov.com/tutorials/java-collections/properties.html): The [Java Properties](https://jenkov.com/tutorials/java-collections/properties.html) class is a special key-value store similar to a [Java Map](https://jenkov.com/tutorials/java-collections/map.html), but specifically targeted at keeping string-string key-value pairs, and being able to load and store properties from property files.
* [Comparable](https://jenkov.com/tutorials/java-collections/comparable.html)
* [Comparator](https://jenkov.com/tutorials/java-collections/comparator.html)

There are two "groups" of interfaces: `Collection`'s and `Map`'s.

Here is a graphical overview of the `Collection` interface hierarchy:

![](https://jenkov.com/images/java-collections/collection-overview.png)

And here is a graphical overview of the `Map` interface hierarchy:

![](https://jenkov.com/images/java-collections/map-overview.png)

