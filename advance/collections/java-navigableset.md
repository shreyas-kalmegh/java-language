# Java NavigableSet

The _Java_ _NavigableSet_ interface, `java.util.NavigableSet`, is a subtype of the [Java SortedSet](https://jenkov.com/tutorials/java-collections/sortedset.html) interface. Therefore the `NavigableSet` behaves like a `SortedSet`, but with an additional set of navigation methods available in addition to the sorting mechanisms of the `SortedSet`.

In Java 6 to 13 there is only one implementation of the `NavigableSet` interface in the `java.util` package: The `java.util.TreeSet` class.



```
NavigableSet navigableSet = new TreeSet();
```

### descendingSet()

The `descendingSet()` method returns a `NavigableSet` in which the order of the elements is reversed compared to this one. The returned "view" is backed by the original `NavigableSet`, so changes to the descending set are also reflected in the original set

```
NavigableSet reverse = original.descendingSet();
```

### descendingIterator()

The `descendingIterator()` method allows you to iterate the elements of the `NavigableSet` (which is also a `SortedSet`) in reverse order, without changing the order of the elements internally.

```
Iterator reverse = original.descendingIterator()
```

### ceiling()

The `ceiling()` method returns the least (smallest) element in this set that is greater than or equal to the element passed as parameter to the `ceiling()` method



```
Object ceiling = original.ceiling("2");
```

### There are other methods. Refer documentation
