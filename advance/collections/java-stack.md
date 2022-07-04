# Java Stack

The Java `Stack` class actually implements the [Java List](https://jenkov.com/tutorials/java-collections/list.html) interface, but you rarely use a `Stack` as a `List` - except perhaps if you need to inspect all elements currently stored on the stack.



### Create a Stack

To use a Java `Stack` you must first create an instance of the `Stack` class. Here is an example of creating a Java `Stack` instance:

```
Stack stack = new Stack();
```

### Push



```
stack.push("1");
```

### Pop



```
String topElement = stack.pop();
```

### Peek



```
String topElement = stack.peek();
```

### Search



```
int index = stack.search("3");     //index = 3
```

### Iterate



```java
Stack<String> stack = new Stack<String>();

stack.push("123");
stack.push("456");
stack.push("789");

Iterator iterator = stack.iterator();
while(iterator.hasNext()){
    Object value = iterator.next();
}
```
