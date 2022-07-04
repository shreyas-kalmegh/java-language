# Java NavigableMap

The _Java_ _NavigableMap_ interface, `java.util.NavigableMap`, is a sub-interface of the\
[`Java SortedMap`](https://jenkov.com/tutorials/java-collections/sortedmap.html) interface. The `NavigableMap` interface has a few extensions to the `SortedSet` interface which makes it possible to navigate the keys and values stored in the map.



### Create a NavigableMap

To create a Java NavigableMap you must create an instance of one of the classes that implements the `NavigableMap` interface. Here is an example of creating an instance of the Java `TreeMap` class which implements the `NavigableMap` interface:

```java
NavigableMap navigableMap = new TreeMap();

// using comparator
Comparator comparator = new MyComparatorImpl();
SortedMap sortedMap = new TreeMap(comparator);
```

### descendingKeySet()

The first interesting navigation method of `NavigableMap` is the `descendingKeySet()` method. The `descendingKeySet()` method returns a [NavigableSet](https://jenkov.com/tutorials/java-collections/navigableset.html) in which the order of the elements is reversed compared to the original key set. The returned "view" is backed by the original `NavigableSet` key Set, so changes to the descending key Set are also reflected in the original set.



```java
NavigableSet reverse = map.descendingKeySet();
```



### descendingMap()

The second interesting navigation method is the `descendingMap()` method. The `descendingMap()` method returns a `NavigableMap` which is a view of the original `Map`. The order of the elements in this view map is reverse of the order of the original map. Being a view of the original map, any changes to this view is also reflected in the original map.

```java
NavigableMap descending = map.descendingMap();
```

### headMap()/tailMap()



```java
NavigableMap original = new TreeMap();
original.put("1", "1");
original.put("2", "2");
original.put("3", "3");

//this headmap1 will contain "1" and "2"
SortedMap headmap1 = original.headMap("3");

//this headmap2 will contain "1", "2", and "3" because "inclusive"=true
NavigableMap headmap2 = original.headMap("3", true);

SortedMap tailMap = navigableMap.tailMap("c");
// value pairs from the NavigableMap for the keys "c", "d" and "e"j
```

### A few more methods

* ceilingKey()
* floorKey()
* higherKey()
* lowerKey()
* celingEntry()
* &#x20;floorEntry()
* &#x20;higherEntry()
* &#x20;lowerEntry()

