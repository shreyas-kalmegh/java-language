# List

The _Java List_ interface, `java.util.List`, represents an ordered sequence of objects. The elements contained in a Java `List` can be inserted, accessed, iterated and removed according to the order in which they appear internally in the Java `List`

### List vs. Set

that the same element can occur more than once in a Java `List`. This is different from a Java `Set` where each element can occur only once.

that the elements in a `List` has an order, and the elements can be iterated in that order. A Java `Set` does not make any promises about the order of the elements kept internally

### List Implementations



Since `List` is an interface you need to instantiate a concrete implementation of the interface in order to use it. You can choose between the following `List` implementations in the Java Collections API:

* java.util.ArrayList
* java.util.LinkedList
* java.util.Vector
* java.util.Stack

### Convert List to Set, Array, List



```java
List<String> list = new ArrayList<>();

list.add("element 1");
list.add("element 2");
list.add("element 3");
list.add("element 3");

// To Set
Set<String> set = new HashSet<>();
set.addAll(list);

// To Array
String[] objects1 = list.toArray(new String[0]);
```



### Convert Array to List

```java
String[] values = new String[]{ "one", "two", "three" };

List<String> list = (List<String>) Arrays.asList(values);
```

### Sort List Using Comparator

If the objects in the Java `List` do not implement the `Comparable` interface, or if you want to sort the objects in another order than their `compare()` implementation, then you need to use a `Comparator` implementation (`java.util.Comparator`). Here is an example of sorting a list of `Car` objects using a `Comparator`.



```java
List<Car> list = new ArrayList<>();

list.add(new Car("Volvo V40" , "XYZ 201845", 5));
list.add(new Car("Citroen C1", "ABC 164521", 4));
list.add(new Car("Dodge Ram" , "KLM 845990", 2));

Comparator<Car> carBrandComparator = new Comparator<Car>() {
    @Override
    public int compare(Car car1, Car car2) {
        return car1.brand.compareTo(car2.brand);
    }
};

// Using Lambda
Comparator<Car> carBrandComparatorLambda      =
    (car1, car2) -> car1.brand.compareTo(car2.brand);

Collections.sort(list, carBrandComparator);
```

### Iterate List Using Java Stream API



```java
Stream<String> stream = stringList.stream();
stream
    .forEach( element -> { System.out.println(element); })j
```
