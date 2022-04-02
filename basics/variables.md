# Variables



### Java Variable Types

In Java there are four types of variables:

* Non-static fields: Objects keep their internal state in non-static fields. Non-static fields are also called instance variables
* Static fields: A static field is a variable that belongs to a class. A static field has the same value for all objects that access it. Static fields are also called class variable
* Local variables: A local variable is a variable declared inside a method.
* Parameters: A parameter is a variable that is passed to a method when the method is called

### Declaration

#### Primitive

```
int myVariable
```

#### Object

```
Integer myVariable;
```

### Assignment

```
myByte   = 127;
String myString = "string value";
```

### Naming Conventions

1. Case Sensitive
2. Java variable names must start with a letter, or the $ or \_ character.
3. After the first character in a Java variable name, the name can also contain numbers (in addition to letters, the $, and the \_ character).
4. Variable names cannot be equal to reserved key words in Java.&#x20;

### Naming Practices(not compiler enforced)

* Variable names are written in camerlCase.
* Even though it is allowed, you do not normally start a Java variable name with $ or \_ .
* Static final fields (constants) are named in all uppercase, typically using an \_ to separate the words in the name. For instance `EXCHANGE_RATE` or `COEFFICIENT`.

### Type Inference

```
var list = new ArrayList();
var myNum = new Integer(123);
var myClassObj = new MyClass();
```

{% hint style="info" %}
JAVA 10 enhancement. This enhancement is restricted to local variables, indexes in for-each loops and local variables declared in for-loops
{% endhint %}
