# Data Types

A variable of a **primitive data type** contains the value of the variable **directly in the memory** allocated to the variable. For instance, a number or a character.

A variable of an o**bject reference type** is different from a variable of a primitive type. A variable of an object type is also called a _reference_. The variable itself does not contain the object, but contains a _**reference**_** to the object**. t is possible to have many different variables reference the same object.

### Primitive Data Types

| **Data type** | **Description**                                                                          |
| ------------- | ---------------------------------------------------------------------------------------- |
| boolean       | A binary value of either `true` or `false`                                               |
| byte          | 8 bit signed value, values from -128 to 127                                              |
| short         | 16 bit signed value, values from -32.768 to 32.767                                       |
| char          | 16 bit Unicode character                                                                 |
| int           | 32 bit signed value, values from -2.147.483.648 to 2.147.483.647                         |
| long          | 64 bit signed value, values from -9.223.372.036.854.775.808 to 9.223.372.036.854.775.808 |
| float         | 32 bit floating point value                                                              |
| double        | 64 bit floating point value                                                              |

### Object Types



| **Data type** | **Description**                                                                          |
| ------------- | ---------------------------------------------------------------------------------------- |
| Boolean       | A binary value of either `true` or `false`                                               |
| Byte          | 8 bit signed value, values from -128 to 127                                              |
| Short         | 16 bit signed value, values from -32.768 to 32.767                                       |
| Character     | 16 bit Unicode character                                                                 |
| Integer       | 32 bit signed value, values from -2.147.483.648 to 2.147.483.647                         |
| Long          | 64 bit signed value, values from -9.223.372.036.854.775.808 to 9.223.372.036.854.775.808 |
| Float         | 32 bit floating point value                                                              |
| Double        | 64 bit floating point value                                                              |
| String        | N byte Unicode string of textual data. Immutable                                         |

When you declare an object reference variable, the reference does not point to any object. You need to create (instantiate) an object first. Here is how that is done:



```
Integer myInteger;
myInteger = new Integer(45);

Integer myInteger = new Integer(45); //or at the same time
```

{% hint style="info" %}
The object versions of the primitive data types are immutable, meaning the values stored inside them cannot be changed once set

The variable that references the object can be made to point to another object though
{% endhint %}

```
Integer myInteger = new Integer(45);

myInteger = new Integer(33); // variable pointing to newo bject
```

### Autoboxing



Before Java 5 you had to call methods on the object versions of the primitive types, to get their value out as a primitive type. For instance:

```
// object to primitive
Integer myInteger = new Integer(45);
int myInt = myInteger.intValue();

// primitive to object
int myInt = 45;
Integer myInteger = new Integer(myInt);
```

From Java 5 you have a concept called "auto boxing".&#x20;

That means that Java can automatically "box" a primitive variable in an object version: Java would automatically extract the `int` value from the `myInteger` object and assign that value to `myInt`.



```
Integer myInteger = new Integer(45);
int myInt = myInteger;
```

, if that is required, or "unbox" an object version of the primitive data type if required.

```
int myInt = 45;
Integer myInteger = myInt;
```

{% hint style="warning" %}
There is one pitfall to keep in mind though. A variable of type object (a reference to an object) can point to `null`, meaning it points to nothing - no object. If you try to convert `null` to a primitive value you will get a `NullPointerException` (an error that causes the program to fail)
{% endhint %}

```
// NullPointerException at runtime
Integer myInteger = null;
int myInt = myInteger;
```
