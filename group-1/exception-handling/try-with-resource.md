# Try With Resource

_Java try-with-resources_, is an exception handling mechanism that can automatically close resources like a Java InputStream or a JDBC Connection when you are done with them.



```
private static void printFile() throws IOException {

    try(FileInputStream input = new FileInputStream("file.txt")) {
            // do something with input
        }
    }
    
    // another way JAVA 9
    FileInputStream input = new FileInputStream("file.txt");
    try(input) { // do something with input }
}
```

### Multiple Resources

```
try(  FileInputStream     input         = new FileInputStream("file.txt");
          BufferedInputStream bufferedInput = new BufferedInputStream(input)
    )
```

#### Closing Order

The resources declared in a Java try-with-resources construct will be closed in reverse order of the order in which they are created / listed inside the parentheses. In the example in the previous section, first thewill be closed, then the `FileInputStream`.

### Custom AutoClosable Implementations

The Java _try-with-resources_ construct does not just work with Java's built-in classes. You can also implement the `java.lang.AutoCloseable` interface in your own classes, and use them with the _try-with-resources_ construct.

The `AutoClosable` interface only has a single method called `close()`. Here is how the interface looks:

```
public interface AutoClosable {

    public void close() throws Exception;
}
```

#### Example



```
public class MyAutoClosable implements AutoCloseable {

    public void doIt() {
        System.out.println("MyAutoClosable doing it!");
    }

    @Override
    public void close() throws Exception {
        System.out.println("MyAutoClosable closed!");
    }
}

// use it
private static void myAutoClosable() throws Exception {

    try(MyAutoClosable myAutoClosable = new MyAutoClosable()){
        myAutoClosable.doIt();
    }
}

// output
MyAutoClosable doing it!
MyAutoClosable closed!
```

### Try With Exception Handling \*\*\*

If an exception is thrown from within a Java _try-with-resources_ block, any resource opened inside the parentheses of the _try_ block will still get closed automatically. The throwing of the exception will force the execution to leave the _try_ block, and this will force the automatic closing of the resource. The exception thrown from inside the _try_ block will get propagated up the call stack, once the resources have been closed.

Some resources may also throw exceptions when you try to close them. In case a resource throws an exception when you try to close it, any other resources opened within the same _try-with-resources_ block will still get closed. After closing all resources, the exception from the failed close-attempt will get propagated up the call stack. In case multiple exceptions are thrown from multiple resource close attempts, the first exception encountered will be the one propagated up the call stack. The rest of the exceptions will be suppressed.

If an exception is thrown both from inside the _try-with-resources_ block, and when a resource is closed (when `close()` is called), the exception thrown inside the _try_ block will be propagated up the call stack. The exception thrown when the resource was attempted closed will be suppressed. This is opposite of what happens in a normal [try-catch-finally](https://jenkov.com/tutorials/java-exception-handling/basic-try-catch-finally.html) block, where the last exception encountered is the exception that is propagated up the call stack.



#### Catch Block

You can add a _catch_ block to a _try-with-resources_ block just like you can to a standard _try_ block. If an exception is thrown from within the _try_ block of a _try-with-resources_ block, the _catch_ block will catch it, just like it would when used with a standard _try_ construct.

Before the _catch_ block is entered, the _try-with-resources_ construct will attempt to close the resources opened inside the _try_ block. In case an exception is thrown when attempting to close one of the resources, these exceptions will be available from the exception's `getSuppressed()` method inside the _catch_ block. Here is an example of a Java _try-with-resources_ block with a _catch_ block attached:

```
try(AutoClosableResource resourceOne = new AutoClosableResource("One", true)) {
    resourceOne.doOp(true);
} catch(Exception e) {
    Throwable[] suppressed = e.getSuppressed();
    throw e;
}
```

#### Finally Block

It is also possible to add a _finally_ block to a Java _try-with-resources_ block. It will behave just like a standard _finally_ block, meaning it will get executed as the last step before exiting the _try-with-resources_ block - after any _catch_ block has been executed.

In case you throw an exception from within the _finally_ block of a _try-with-resources_ construct, all previously thrown exceptions will be lost!

#### Adding Suppressed Exceptions Manually

Skipped
