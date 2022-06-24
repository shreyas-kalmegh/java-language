# Collections Utility Methods

### addAll()

```
List<String> list = new ArrayList<>();

Collections.addAll(list, "element 1", "element 2", "element 3");
```

### binarySearch()

The `Collections` `binarySearch()` method can search a [Java List](https://jenkov.com/tutorials/java-collections/list.html) for an element using a binary search algorithm. The `List` must be sorted in ascending order before you search it using `binarySearch()`

```
List<String> list = new ArrayList<>();
list.add("one");
list.add("two");
list.add("three");
list.add("four");
list.add("five");

Collections.sort(list);

int index = Collections.binarySearch(list, "four");

System.out.println(index);
```



### copy()

The `Collections` `copy()` method can copy all elements of a `List` into another `List`. Here is a Java example of calling the `Collections` `copy()` method:

```
List<String> source = new ArrayList<>();
Collections.addAll(source, "e1", "e2", "e3");

List<String> destination = new ArrayList<>();
Collections.copy(destination, source);
```



### reverse()

The `Collections` `reverse()` method can reverse the elements in a Java `List`. Here is an example of reversing the elements of a `List`:

```
List>String< list = new ArrayList<String>();

list.add("one");
list.add("two");
list.add("three");

Collections.reverse(list);
```



### shuffle()

The `Collections` `shuffle()` method can shuffle the elements of a `List`. Here is an example of shuffling a list with the `Collections` `shuffle()` method:

```
List>String< list = new ArrayList<String>();

list.add("one");
list.add("two");
list.add("three");

Collections.shuffle(list);
```



### sort()

The `Collections` `sort()` method can sort a Java `List`. I have covered sorting of `List`s in my [sort Java List tutorial](https://jenkov.com/tutorials/java-collections/sorting.html). Here is an example of sorting a Java `List` using `Collections` `sort()` method:

```
List>String< list = new ArrayList<String>();

list.add("one");
list.add("two");
list.add("three");
list.add("four");

Collections.sort(list);
```

### min()

The `Collections` `min()` method can find the minimum element in a `List` according to the natural ordering of the elements (see my [Java List sorting tutorial](https://jenkov.com/tutorials/java-collections/sorting.html)). Here is an example of finding the minimum element in a Java `List` using `Collections` `min()` method:

```
List source = new ArrayList();
source.add("1");
source.add("2");
source.add("3");

String min = (String) Collections.min(source);
```

After running the code above, the `min` variable will contain the String value `1` .

### max()

The `Collections` `max()` method can find the maximum element in a `List` according to the natural order of the elements (see my [Java List sorting tutorial](https://jenkov.com/tutorials/java-collections/sorting.html)). Here is an example of finding the maximum element in a Java `List`:

```
List source = new ArrayList();
source.add("1");
source.add("2");
source.add("3");

String max = (String) Collections.max(source);
```

After running the code above, the `max` variable will contain the String value `3` .

### replaceAll()

The Java `Collections` `replaceAll()` method can replace all occurrences of one element with another element.

he `Collections` `replaceAll()` method returns `true` if any elements were replaced, and `false` if not



### unmodifiableSet()

The `unmodifiableSet()` method in the Java `Collections` class can create an immutable (unmodifiable) `Set` from a normal [Java Set](https://jenkov.com/tutorials/java-collections/set.html) . Here is a Java example of creating an immutable `Set` from a normal `Set`:

```
Set normalSet    = new HashSet();

Set immutableSet = Collections.unmodifiableSet(normalSet);
```
