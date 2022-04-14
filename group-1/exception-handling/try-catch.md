# Try Catch

Exceptions are used in a program to signal that some error or exceptional situation has occurred, and that it doesn't make sense to continue the program flow until the exception has been handled.

### Throwing Exceptions

If a method needs to be able to throw an exception, it has to declare the exception(s) thrown in the method signature, and then include a throw-statement in the method. Here is an example:

```
    public void divide(int numberToDivide, int numberToDivideBy)
    throws BadNumberException{
        if(numberToDivideBy == 0){
            throw new BadNumberException("Cannot divide by 0");
        }
        return numberToDivide / numberToDivideBy;
    }
```

{% hint style="info" %}
You can throw any type of exception from your code, as long as your method signature declares it. You can also make up your own exceptions. Exceptions are regular Java classes that extends java.lang.Exception, or any of the other built-in exception classes. If a method declares that it throws an exception A, then it is also legal to throw subclasses of A.
{% endhint %}



### Catching Exceptions

If a method calls another method that throws checked exceptions, the calling method is forced to either pass the exception on, or catch it. Catching the exception is done using a try-catch block. Here is an example:

```
    public void callDivide(){
        try {
            int result = divide(2,1);
            System.out.println(result);
        } catch (BadNumberException e) {
            //do something clever with the exception
            System.out.println(e.getMessage());
        } catch (someException) {
            // multiple catch block supported
        }  catch(SQLException | IOException e) {
            // multiple Exceptions in the same catch block JAVA 7
        }
        System.out.println("Division attempt done");
    }
```

If an exception is thrown inside the catch-block and that exception is not caught, the catch-block is interrupted just like the try-block would have been.

When the catch block is finished the program continues with any statements following the catch block. In the example above the "System.out.println("Division attempt done");" statement will always get executed



### Propagating Exceptions

You don't have to catch exceptions thrown from other methods. If you cannot do anything about the exception where the method throwing it is called, you can just let the method propagate the exception up the call stack to the method that called this method. If you do so the method calling the method that throws the exception must also declare to throw the exception. Here is how the callDivide() method would look in that case.

```
    public void callDivide() throws BadNumberException{
        int result = divide(2,1);
        System.out.println(result);
    }
```



### Finally

You can attach a finally-clause to a try-catch block. The code inside the finally clause will always be executed, even if an exception is thrown from within the try or catch block. If your code has a return statement inside the try or catch block, the code inside the finally-block will get executed before returning from the method. Here is how a finally clause looks:

```
    public void openFile(){
        FileReader reader = null;
        try {
            reader = new FileReader("someFile");
            int i=0;
            while(i != -1){
                i = reader.read();
                System.out.println((char) i );
            }
        } catch (IOException e) {
            //do something clever with the exception
        } finally {
            if(reader != null){
                try {
                    reader.close();
                } catch (IOException e) {
                    //do something clever with the exception
                }
            }
            System.out.println("--- File End ---");
        }
    }
```

### Catch or Propagate Exceptions?

&#x20;In many applications you can't really do much about the exception but tell the user that the requested action failed. In these applications you can usually catch all or most exceptions centrally in one of the first methods in the call stack. You may still have to deal with the exception while propagating it though (using finally clauses). For instance, if an error occurs in the database connection in a web application, you may still have to close the database connection in a finally clause, even if you can't do anything else than tell the user that the action failed.
