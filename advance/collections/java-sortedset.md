# Java SortedSet

The _Java_ _SortedSet_ interface, `java.util.SortedSet`, is a subtype of the [`java.util.Set`](https://jenkov.com/tutorials/java-collections/set.html) interface. The Java `SortedSet` interface behaves like a normal `Set` with the exception that the elements it contains are sorted internally

The Java Collections API only has one implementation of the Java `SortedSet` interface - the `java.util.TreeSet` class.

### Create a TreeSet With a Comparator

It it possible to pass a `Comparator`, `java.util.Comparator` implementation to the constructor of the `TreeSet`. This `Comparator` will then decide the ordering of the elements in the `TreeSet`

``

```java
Comparator comparator = new MyComparatorImpl();

SortedSet sortedSet = new TreeSet(comparator);
```

### Ascending vs. Descending Sort Order

By default the elements of a `SortedSet` are iterated in ascending order`.` But it is also possible to iterate the elements in descending order using the method `TreeSet.descendingIterator()`.



```java
TreeSet treeSet = new TreeSet();

treeSet.add("one");
treeSet.add("two");
treeSet.add("three");

Iterator iterator = treeSet.descendingIterator();
while(iterator.hasNext()) {
    String element = (String) iterator.next();
    System.out.println(element);
}
```



### Get Comparator Used

If you created your `SortedSet` with a `Comparator`, you can obtain that `Comparator` via the `SortedSet` `comparator()` method.

```
Comparator comparator = sortedSet.comparator();
```

### Get First/Last Element



```
Object firstElement = sortedSet.first();
Object lastElement = sortedSet.last();
```

### Get Head`/Tail` Set

The Java `SortedSet` interface has a method named `headSet()` which returns another `SortedSet` with all elements that are smaller than (ahead of) a given parameter value, according to the sort order used by the `SortedSet`

The Java `SortedSet` interface has a method named `setSet()` which returns another `SortedSet` with all elements that are greater than or equal to (tailing) a given parameter value, according to the sort order used by the `SortedSet`

``

```
SortedSet headSet = sortedSet.headSet("c");
```

### Get Subset

The returned subset will contain all elements equal to or greater than the first parameter, and smaller than the second parameter, according to the sort order used by the `SortedSet`

``

```
SortedSet subSet = sortedSet.subSet("c", "e");
```
