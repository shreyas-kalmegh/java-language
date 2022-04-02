# Control Flow

### if Else



```
if( name.equals("john")) {
    //...
} else if ( name.equals("jane")) {
    //...
} else if ( name.equals("Linda")) {
    //...
} else {
    //...
}
```



If the block of code to be executed is just a single statement, you do not need the brackets `{ }` around them, in the `if` statements. Here is an example: (**Avoid this**)

```
if ( isValid )   System.out.println("it is valid");
else             System.out.println("it is not valid");
```

### Ternery Operator



The _Java_ _ternary operator_ functions like a simplified [Java if](http://tutorials.jenkov.com/java/if.html) statement. The ternary operator consists of a condition that evaluates to either `true` or `false`, plus a value that is returned if the condition is `true` and another value that is returned if the condition is `false`. Here is a simple Java ternary operator example:

```
String case = ... // get this string from somewhere, e.g. a parameter or program arg


String name = case.equals("uppercase") ? "JOHN" : "john";
```



#### Ternary Operator as Null Check

You can use the Java ternary operator as a shorthand for null checks before calling a method on an object. Here is an example:

```
String value = object != null ? object.getValue() : null;
```



#### Ternary Operator as max Function

You can achieve the same functionality as the [Java Math max() function](http://tutorials.jenkov.com/java/math-operators-and-math-class.html#math-max) using a Java ternary operator. Here is an example of achieving the `Math.max()` functionality using a Java ternary operator:

```
int val1 = 10;
int val2 = 20;

int max = val1 >= val2 ? val1 : val2;
```



#### Chained Ternary Operators

It is possible to chain more than one Java ternary operator together. You do so by having one of the values returned by the ternary operator be another ternary operator. Here is an example of a chained ternary operator in Java:

```
String input = ... // get input parameter String from somewhere.

int value = input == null ? 0 : input.equals("") ? 0 : Integer.parseInt(input);
```



### Java Switch Statement Example

```
int amount = 9;

switch(amount) {
    case     0 : System.out.println("amount is  0"); break;
    case     5 : System.out.println("amount is  5"); break;
    case    10 : System.out.println("amount is 10"); break;
    default    : System.out.println("amount is something else");
}
```

{% hint style="info" %}
Before Java 7 this variable has to be numeric and must be either a `byte`, `short`, `char` or `int`. From Java 7 the variable can also be a `String` It is also possible switch on a [Java enum](http://tutorials.jenkov.com/java/enums.html) variable
{% endhint %}



#### Multiple case statements for same operation

In case you want the same operation executed for multiple `case` statements, you write it like this:

```
char key = '\t'

switch(key) {
    case ' '  :
    case '\t' : System.out.println("white space char");
                break;

    default   : System.out.println("char is something else");
}
```



#### Multiple Values Per Case Statement

From Java 13 and forward you can also have multiple values per `case` statement, instead of having multiple case statements falling through to the next. Here is the example from the previous section rewritten to use multiple values in a single `state` statement:

```
char key = '\t'

switch(key) {
    case     ' ', '\t' :
             System.out.println("white space char");
             break;

    default: System.out.println("char is something else");
}
```
