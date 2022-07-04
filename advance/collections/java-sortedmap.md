# Java SortedMap

The _Java_ _SortedMap_ interface, `java.util.SortedMap`, is a subtype of the [java.util.Map](https://jenkov.com/tutorials/java-collections/map.html) interface, with the addition that the elements stored in a Java `SortedMap` map are sorted internally. This means you can iterate the elements stored in a _SortedMap_ in the sort order. &#x20;

#### Create a TreeMap\`

You instantiate a `TreeMap` instance via its constructor. Here is an example of creating a Java `TreeMap` instance, which implements the `SortedMap` interface:

```java
SortedMap sortedMap = new TreeMap();

// with a comparator
Comparator comparator = new MyComparatorImpl();

SortedMap sortedMap = new TreeMap(comparator);
```

### Sort Order

The order of the sorting in a Java _SortedMap_ is either the natural sorting order of the elements (if they implement `java.lang.Comparable`), or the order determined by a `Comparator` that you can give to the `SortedSet`.



### Iterate a SortedMap

You iterate a Java `SortedMap` just like you iterate a normal Java `Map`. Since the keys of a `SortedMap` are sorted, you will most likely want to iterate the keys in their sorted order. You iterate the keys of a `SortedMap` by calling its `keySet()` method, like this:

```java
SortedMap sortedMap = new TreeMap();

sortedMap.put("a", "one");
sortedMap.put("b", "two");
sortedMap.put("c", "three");

Iterator iterator = sortedMap.keySet().iterator();

while(iterator.hasNext()) {
    String key   = (String) iterator.next();

    String value = (String) sortedMap.get(key);
}

// iterate in descending
Iterator iterator = sortedMap.descendingKeySet().iterator();

while(iterator.hasNext()) {
    String key   = (String) iterator.next();

    String value = (String) sortedMap.get(key);
}
```

&#x20;   &#x20;

### Get Comparator Used

If your Java `SortedMap` was created using a `Comparator`, you can obtain the `Comparator` used via the `SortedMap` `comparator()` method. Here is an example of obtaining the `Comparator` used by a `SortedMap` via its `comparator()` method:

```java
Comparator comparator = sortedMap.comparator();
```

### Get First/ Last Key

The `SortedMap` interface has a shortcut method to obtain the first (lowest)/last (highest) key in the key set of the `SortedMap`.&#x20;

```java
String firstKey = (String) sortedMap.firstKey();
String lastKey = (String) sortedMap.lastKey();
```

### Head Map/ Tail Map

The `SortedMap` interface has method named `headMap()/tailMap` which returns a new `Map` which contains the first/last elements of the `SortedMap` according to the sort order used.

All elements with a key that is smaller than / earlier than the parameter passed to the `headMap()` method

All elements with a key that is equal to or larger than the parameter passed to the `tailMap()` method



```java
SortedMap sortedMap = new TreeMap();

sortedMap.put("a", "1");
sortedMap.put("c", "3");
sortedMap.put("e", "5");
sortedMap.put("d", "4");
sortedMap.put("b", "2");

SortedMap headMap = sortedMap.headMap("c");
System.out.println(headMap);
// ("a", "1") and ("b", "2")

SortedMap tailMap = sortedMap.tailMap("c");
System.out.println(tailMap);
// ("c", "3"), ("d", "4") and ("e", "5")
```

### Submap

The Java `SortedMap` also has a method named `subMap()` which can return a new `Map` which is a submap of the `SortedMap`. The `subMap()` method takes two parameters which act as delimiters for what elements are included in the returned submap.

equal to or larger than the first parameter, and smaller than the second parameter



```java
SortedMap sortedMap = new TreeMap();

sortedMap.put("a", "1");
sortedMap.put("c", "3");
sortedMap.put("e", "5");
sortedMap.put("d", "4");
sortedMap.put("b", "2");

SortedMap subMap = sortedMap.subMap("b", "e");
System.out.println(subMap);
// ("b", "2), ("c", "3") and ("d", "4")
```
