# Deque

The _Java_ _Deque_ interface, `java.util.Deque`, represents a double ended queue, meaning a queue where you can add and remove elements to and from both ends of the queu

Because you can enqueue and dequeue from both ends of a Java Deque, you can use a Deque as both a queue and a stack. The Java `Deque` interface extends the [Java Queue](https://jenkov.com/tutorials/java-collections/queue.html) interface. That means that you can use all the Java Queue methods when working with a Deque. The Deque interface does not extend the [Java Stack](https://jenkov.com/tutorials/java-collections/stack.html) interface, but the Deque interface defines methods that enable you to do the same operations you would normally do on a stack (push, peek, pop).



Since Java `Deque` is an interface you need to instantiate a concrete implementation of the interface in order to use it. You can choose between the following `Deque` implementations in the Java Collections API:

* java.util.LinkedList
* java.util.ArrayDeque



```java
Deque deque = new LinkedList();
Deque deque = new ArrayDeque();
```



### Add Element to Deque

As mentioned in the beginning of this Java `Deque` tutorial, you can add elements to both the beginning and end of a `Deque`. The Java `Deque` interface contains the following methods for adding elements to it:

* add(): You add elements to the end (tail) of a `Deque` using the `add()` method.
* addLast(): The `addLast()` method also adds an element to the end (tail) of a Java `Deque`.
* addFirst(): To add an element at the beginning (head) instead of the end of a Java `Deque` you call the `addFirst()` method instead.If the element cannot be added to the beginning of the Deque, the `addFirst()` method will throw an exception. This is different from the `offerFirst()` method which will return `false` if an element cannot be inserted in the beginning of the Deque.
* offer(): The `offer()` method adds an element to the end (tail) of the Deque. If adding the element succeeds the `offer()` method returns `true`. If the adding the element fails - e.g. if the Deque is full, the `offer()` method returns `false`. This is different from the `add()` method which will throw an exception is adding an element to the end of the Deque fails.
* offerFirst()
* offerLast(): The `offerLast()` method adds an element to the end (tail) of the Deque, just like `offer()`.

