# Java Queue

The _Java_ _Queue_ interface, `java.util.Queue` represents a data structure designed to have elements inserted at the end of the queue, and elements removed from the beginning of the queue

Since `Queue` is an interface you need to instantiate a concrete implementation of the interface in order to use it. You can choose between the following `Queue` implementations in the Java Collections API:

* java.util.LinkedList
* java.util.PriorityQueue

`LinkedList` is a pretty standard queue implementation. Elements in the queue are stored internally in a standard linked list data structure. This makes it fast to insert elements at the end (tail) of the list, and remove elements from the beginning (head) of the list.

`PriorityQueue` stores its elements internally according to their natural order (if they implement `Comparable`), or according to a `Comparator` passed to the `PriorityQueue`.



```java
Queue queueA = new LinkedList();
Queue queueB = new PriorityQueue();
```

### Add Element to Queue

The `add()` and `offer()` methods differ in how the behave if the Queue is full, so no more elements can be added. The `add()` method throws an exception in that case, whereas the `offer()` method just returns `false`

``

```java
Queue<String> queue = new LinkedList<>();

queue.add("element 1");

queue.offer("element 2")
```

### Take Element From Queue

The `poll()` method returns `null` if the Queue is empty. The `remove()` method throws an exception if the Queue is empty.



```java
Queue<String> queue = new LinkedList<>();

queue.add("element 1");
queue.add("element 2");

String element1 = queue.poll();

String element2 = queue.remove();
```

### Peek at the Queue

The `element()` method returns the first element in the `Queue`. If the `Queue` is empty, the `element()` method throws a `NoSuchElementException`

The `peek()` works like the `element()` method except it does not throw an exception if the `Queue` is empty. Instead it just returns `null`

```java
String firstElement = queue.element();
String firstElement = queue.peek();
```

### Remove Element From Queue

To remove elements from a Java `Queue`, you call the `remove()` method. This method removes the element at the head of the `Queue`

```java
String removedElement = queue.remove();
```

### Remove All Elements From Queue

You can remove all elements from a Java Queue using its `clear()` method.

```java
queue.clear();
```

### Get Queue Size

```java
int size = queue.size();
```

### Check if Queue Contains Element



```java
boolean containsHonda = queue.contains("Honda");
```

### Iterate All Elements in Queue



```java
Queue<String> queue = new LinkedList<>()

//access via Iterator
Iterator<String> iterator = queue.iterator();
while(iterator.hasNext(){
  String element = iterator.next();
}

//access via new for-loop
for(String element : queue) {
    //do something with each element
}
```
