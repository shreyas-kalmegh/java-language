# Arrays

A _Java Array_ is a collection of variables of the same type. For instance, an _array_ of `int` is a collection of variables of the type `int`. The variables in the array are ordered and each have an index.&#x20;

![Java arrays are collections of variables of the same type, ordered with an index.](http://tutorials.jenkov.com/images/java/java-arrays-1.png)

You can use a Java array as a [field](http://tutorials.jenkov.com/java/fields.html), static field, a local variable, or parameter, just like any other variable. An array is simply a variation of the data type.

### Declaration

```
int[] intArray;
int   intArray[];

String[] stringArray;
String   stringArray[];

MyClass[] myClassArray;
MyClass   myClassArray[];
```

### Instantiation

```
int[] intArray; // declare

intArray = new int[10]; //instantiate

String[] stringArray = new String[10]; // at the same time
```

{% hint style="info" %}
When you first create an array of object references, each of the cells in the array points to `null` - no object.
{% endhint %}

### Java Array Literals

The Java programming language contains a shortcut for instantiating arrays of **primitive types and strings**. If you already know what values to insert into the array, you can use an array literal

```
int[]   ints2 = new int[]{ 1,2,3,4,5,6,7,8,9,10 };
```

### Array Length

You can access the length of an array via its `length` field. Here is an example:

```
int[] intArray = new int[10];
int arrayLength = intArray.length;
```

### Loop

You can loop through all the elements of an array using the [Java for loop](http://tutorials.jenkov.com/java/for.html). Here is an example of iterating an array with a `for` loop in Java:

```
String[] stringArray = new String[10];

for(int i=0; i < stringArray.length; i++) {
    stringArray[i] = "String no " + i;
}

for(int i=0; i < stringArray.length; i++) {
    System.out.println( stringArray[i] );
}
```

### Multidimensional



You create a multidimensional array in Java by appending one set of square brackets (`[]`) per dimension you want to add. Here is an example that creates a two-dimensional array:

```
int[][] intArray = new int[10][20];
```

####

### The Arrays Class

Java contains a special utility class that makes it easier for you to perform many often used array operations like copying and sorting arrays, filling in data, searching in arrays etc. The utility class is called `Arrays` and is located in the standard Java package `java.util`. Thus, the fully qualified name of the class is:

```
java.util.Arrays
```

### Copying Arrays

```
// without uitlity class
for(int i=0; i < source.length; i++) {
    dest[i] = source[i];
}

// array utility class
int[] dest = Arrays.copyOf(source, source.length);

// copy range: Arrays.copyOfRange(sourceArray, startIndex, endIndex
int[] dest = Arrays.copyOfRange(source, 0, source.length);
```

### Converting Arrays to Strings With Arrays.toString()

```
int[]   ints = new int[10];
for(int i=0; i < ints.length; i++){
    ints[i] = 10 - i;
}
System.out.println(java.util.Arrays.toString(ints));

//output: [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

```



### Sorting Arrays

You can sort the elements of an array using the `Arrays.sort()` method.

```
int[]   ints = new int[10];
for(int i=0; i < ints.length; i++){
    ints[i] = 10 - i;
}
java.util.Arrays.sort(ints);

```

{% hint style="info" %}
The `Arrays.sort()` example shown earlier only works for Java arrays of primitive data types. Java's primitive data types have a natural ordering
{% endhint %}

Objects may not have any natural sort order, so you need to provide another object which is capable of determining the order of your objects. Such an object is called a `Comparator`.

### Sort Arrays of Object Types Example

Here is first the class for the objects we want to sort:

```
// declare class
private static class Employee{
    public String name;
    public int    employeeId;

    public Employee(String name, int employeeId){
        this.name       = name;
        this.employeeId = employeeId;
    }
}

// instantiate it
Employee[] employeeArray = new Employee[3];

employeeArray[0] = new Employee("Xander", 1);
employeeArray[1] = new Employee("John"  , 3);
employeeArray[2] = new Employee("Anna"  , 2);

// sort by providing comparator interface
java.util.Arrays.sort(employeeArray, new Comparator<Employee>() {
    @Override
    public int compare(Employee e1, Employee e2) {
        return e1.name.compareTo(e2.name);
    }
});
```

### Filling Arrays With Arrays.fill()

```
int[] intArray = new int[10];
Arrays.fill(intArray, 123);
System.out.println(Arrays.toString(intArray));

// output: [123, 123, 123, 123, 123, 123, 123, 123, 123, 123]

// partial fill
Arrays.fill(ints2, 3, 5, 123);
System.out.println(Arrays.toString(intArray));

// output: [0, 0, 0, 123, 123, 0, 0, 0, 0, 0]
```

### Searching Arrays with Arrays.binarySearch()



```
int[] ints = {0,2,4,6,8,10};
int index = Arrays.binarySearch(ints, 6);
System.out.println(index);
// output: 3

int index = Arrays.binarySearch(ints, 7);
System.out.println(index);
//output: -5

```

1. The `binarySearch()` method will return the index in the array in which the element was found
2. If more than one element exists in the array with the searched value, there is no guarantee about which element will be found.
3. If no element is found with the given value, a negative number will be returned. The negative number will be the index at which the searched element would be inserted, and then minus one.

The `Arrays.binarySearch()` method also exists in a version where you just search part of the array. Here is how that looks:

```
int[] ints = {0,2,4,6,8,10};
int index = Arrays.binarySearch(ints, 0, 4, 2);
System.out.println(index);
```

will return -5 and not -7 like `binarySearch(ints, 12)` would have

This version of `binarySearch()` works just like the other version, except in the cases where no matching element is found. If no element is found matching within the index interval, then `binarySearch()` will still return the index of where the value should have been inserted. But, if all values in the interval are smaller than the sought value, `binarySearch()` will return -toIndex -1 , and not -array length - 1.

### Checking if Arrays are Equal with Arrays.equals()

```
boolean ints1EqualsInts2 = Arrays.equals(ints1, ints2);
```
