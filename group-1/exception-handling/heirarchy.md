# Heirarchy

The hierarchy is created by having one (or more) exception extend another exception. The first exception becomes a subclass of the second. In Java FileNotFoundException is a subclass of IOException. Here is how a custom exception looks in Java code:

```
public class MyException extends Exception{
    //constructors etc.
}
```

&#x20;The advantage of exception hierarchies is that if you decide to catch (using try-catch) a certain exception in the hierarchy, then you will automatically also catch all subclasses of that exception too. In other words, you will catch all exceptions from that certain exception and down the hierarchy. In the example with FileNotFoundException, if you catch IOException which is the superclass of FileNotFoundException, you will also catch FileNotFoundException.
