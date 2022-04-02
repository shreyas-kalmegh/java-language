# Strings

### Internal String Representation

A Java String (before Java 9) is represented internally in the Java VM using bytes, encoded as UTF-16. UTF-16 uses 2 bytes to represent a single character. Thus, the characters of a Java String are represented using a `char` array.

{% hint style="info" %}
From [Java 9](http://tutorials.jenkov.com/java/index.html#new-in-java-9) and forward, The Java VM can optimize strings using a new Java feature called _compact strings_. The compact strings  lets the Java VM detect if a string only contains ISO-8859-1/Latin-1 characters. If it does, the String will only use 1 byte per character internally. The characters of a compact Java String can thus be represented by a **`byte` array instead of a `char` array**.

Whether a String can be represented as a compact string or not is detected when the string is created. A String is **immutable once created** - so this is safe to do.
{% endhint %}



### Creating a String

Strings in Java are objects. Therefore you need to use the `new` operator to create a new Java String object. Here is a Java String instantiation (creation) example:

```
String myString = new String("Hello World");
String myString = "Hello World"; // using string literals 
```

Escape Characters

Java Strings literals accepts a set of escape characters which are translated into special characters in the created String. These escape characters are:&#x20;

* \\\ Translated into a single \ character in the String&#x20;
* \t Translated into a single tab character in the string&#x20;
* \r Translated into a single carriage return character in the string&#x20;
* \n Translated into a single new line character in the string



### String Literals as Constants or Singletons

If you use the same string (e.g. `"Hello World"`) in other String variable declarations, the Java virtual machine may only create a single String instance in memory. The string literal thus becomes a de facto constant or singleton. The various different variables initialized to the same constant string will point to the same String instance in memory. Here is a Java String constant / singleton example:

```
String myString1 = "Hello World";
String myString2 = "Hello World";
```

{% hint style="info" %}
More precisely, objects representing Java String literals are obtained from a constant String pool which the Java virtual machine keeps internally. That means, that even classes from different projects compiled separately, but which are used in the same application may share constant String objects. The sharing happens at runtime. It is not a compile time feature.
{% endhint %}



If you want to be sure that two String variables point to separate String objects, use the `new` operator like this:

```
String myString1 = new String("Hello World");
String myString2 = new String("Hello World");
```



### Java Text Blocks

_Java_ _text blocks_, also known as _Java_ _multi line strings_, is a feature that was added in Java 13 (in preview) which enables you to more easily declare String literals that span multiple lines in your Java code. To explain the Java text block syntax, look at this Java text block example:

```
String textblock = """
                   This is a text inside a
                   text block
                   """;
```

Both sets of quote characters should be located on their own lines - above and below the actual text to be included in the text block. Only the text on the lines between the lines with the delimiter characters is being included in the resulting Java String.

### Java Text Block Indentation

The indentation of the quote characters on this last line determines how many indentation characters the Java compiler strips out of the text inside the text block.



```
String textblock1 = """
                   This is a Java text block
                   """;

String textblock2 = """
                   This is a Java text block
                 """;

String textblock3 = """
                   This is a Java text block
               """;

System.out.println(textblock1);
System.out.println(textblock2);
System.out.println(textblock3);

// output
This is a Java text block

  This is a Java text block

    This is a Java text block

```



### Concatenating Strings

Strings in Java are immutable meaning they cannot be changed once created. Therefore, when concatenating two Java String objects to each other, the result is actually put into a third String object.

```
String one = "Hello";
String two = "World";

String three = one + " " + two;
```

### String Concatenation Performance



When concatenating Strings you have to watch out for possible performance problems. Concatenating two Strings in Java will be translated by the Java compiler to something like this:

```
String one = "Hello";
String two = " World";

String three = new StringBuilder(one).append(two).toString();
```



Here is a loop containing the above type of String concatenation:

```
String[] strings = new String[]{"one", "two", "three", "four", "five"};

String result = null;
for(String string : strings) {
    result = result + string;
}
```

This code will be compiled into something similar to this:

```
String[] strings = new String[]{"one", "two", "three", "four", "five"};

String result = null;
for(String string : strings) {
    result = new StringBuilder(result).append(string).toString();
}
```



The fastest way of concatenating Strings is to create a `StringBuilder` once, and **reuse** the same instance inside the loop. Here is how that looks:

```
String[] strings = new String[]{"one", "two", "three", "four", "five"};

StringBuilder temp  = new StringBuilder();
for(String string : strings) {
    temp.append(string);
}
String result = temp.toString();
```



### String Length

You can obtain the length of a String using the `length()` method. The length of a String is the number of characters the String contains - not the number of bytes used to represent the String. Here is an example:

```
String string = "Hello World";
int length = string.length();
```

### Substrings

You can extract a part of a String. This is called a substring. You do so using the `substring()` method of the String class. **"from - including, to - **_**excluding**_**"**

```
String string1 = "Hello World";

String substring = string1.substring(0,5);
```



### Searching in Strings With indexOf()

You can search for substrings in Strings using the `indexOf()` method. Here is an example:

The `indexOf()` method returns the index of where the first character in the first matching substring is found. In this case the `W` of the matched substring `World` was found at index `6`.

If the substring is not found within the string, the `indexOf()` method returns `-1`

```
String string1 = "Hello World";

int index = string1.indexOf("World");
```

There is a version of the `indexOf()` method that takes an index from which the search is to start

```
theString.indexOf(substring, index + 1);
```

{% hint style="info" %}
There is also lastIndexOf(

```
int index = theString.lastIndexOf(substring);
```
{% endhint %}



### Matching a String Against a Regular Expression With matches()

The Java String `matches()` method takes a regular expression as parameter, and returns `true` if the regular expression matches the string, and `false` if not.

```
String text = "one two three two one";

boolean matches = text.matches(".*two.*");
```



### Comparing Strings

Java Strings also have a set of methods used to compare Strings. These methods are:

* equals()
* equalsIgnoreCase()
* startsWith()
* endsWith()
* compareTo()
* equalsIgnoreCase()



#### compareTo()

The `compareTo()` method compares the String to another String and returns an `int` telling whether this String is smaller, equal to or larger than the other String. If the String is earlier in sorting order than the other String, `compareTo()` returns a negative number. If the String is equal in sorting order to the other String, `compareTo()` returns 0. If the String is after the other String in sorting order, the `compareTo()` metod returns a positive number.

Here is an example:

```
String one   = "abc";
String two   = "def";
String three = "abd";

System.out.println( one.compareTo(two)   );
System.out.println( one.compareTo(three) );

// ouput
-3
-1

```



### Trimming Strings With trim()

The Java String class contains a method called `trim()` which can trim a string object. By _trim_ is meant to remove white space characters at the beginning and end of the string. White space characters include space, tab and new lines. Here is a Java String `trim()` example:

```
String text    = "  And he ran across the field   ";
String trimmed = text.trim();

// ouput
"And he ran across the field"
```

### Replacing Characters in Strings With replace()

The Java String class contains a method named `replace()` which can replace characters in a String.

```
String source   = "123abc";
String replaced = source.replace('a', '@');

//output
123@bc
```

The replace() method will replace all character matching the character passed as first parameter to the method, with the second character passed as parameter to the replace() method.

#### replaceFirst()

The Java String `replaceFirst()` method returns a new String with the first match of the regular expression passed as first parameter with the string value of the second parameter.

```
String text = "one two three two one";
String s = text.replaceFirst("two", "five");

// output
"one five three two one".
```

#### replaceAll()

The Java String `replaceAll()` method returns a new String with all matches of the regular expression passed as first parameter with the string value of the second parameter.

```
String text = "one two three two one";
String t = text.replaceAll("two", "five");

// output
 "one five three five one".
```



### Splitting Strings With split()

The Java String class contains a `split()` method which can be used to split a String into an [array](http://tutorials.jenkov.com/java/arrays.html) of String objects. Here is a Java String `split()` example:

```
String   source = "A man drove with a car.";
String[] occurrences = source.split("a");

// output
"A m"
"n drove with "
" c"
"r."
```



The String `split()` method exists in a version that takes a `limit` as a second parameter. Here is a Java String `split()` example using the `limit` parameter:

```
String   source = "A man drove with a car.";
int      limit  = 2;
String[] occurrences = source.split("a", limit);

// output
"A m"
"n drove with a car."
```



### Converting Numbers to Strings With valueOf()

The Java String class contains a set of overloaded static methods named `valueOf()` which can be used to convert a number to a String. Here are some simple Java String `valueOf()` examples:

```
String intStr = String.valueOf(10);
System.out.println("intStr = " + intStr);

String flStr = String.valueOf(9.99);
System.out.println("flStr = " + flStr);

// output
intStr = 10
flStr = 9.99
```



### Converting Objects to Strings

The Object class contains a method named `toString()`. Since all Java classes extends (inherits from) the Object class, all objects have a `toString()` method. This method can be used to create a String representation of the given object. Here is a Java `toString()` example:

```
Integer integer = new Integer(123);

String intStr = integer.toString();
```

{% hint style="info" %}
For the `toString()` method to return a sane String representation of the given object, the class of the object must have overridden the `toString()` method. If not, the default `toString()` method (inherited from the Object class) will get called
{% endhint %}



### Getting Characters and Bytes

It is possible to get a character at a certain index in a String using the `charAt()` method. Here is an example:

```
String theString = "This is a good day to code";

System.out.println( theString.charAt(0) );
System.out.println( theString.charAt(3) );

// output 
T
s

byte[] bytes1 = theString.getBytes();
byte[] bytes2 = theString.getBytes(Charset.forName("UTF-8");
```



### Converting to Uppercase and Lowercase

You can convert Strings to uppercase and lowercase using the methods `toUpperCase()` and `toLowerCase()`. Here are two examples:

```
String theString = "This IS a mix of UPPERcase and lowerCASE";

String uppercase = theString.toUpperCase();
String lowercase = theString.toLowerCase();
```



### String Formatting

From Java 13 the Java String class got a new method named `formatted()` which can be used to return a _formatted_ version of the String `formatted()` is called on. The `formatted()` method is only a preview feature that was added together with Java Text Blocks in Java 13, so we do not yet know if it will stay in. Here is an example of using the Java String `formatted()` method:

```
String input = "Hello %s";

String output1 = input.formatted("World");
System.out.println(output1);

String output2 = input.formatted("Jakob");
System.out.println(output2);
```



### Strip Indentation

From Java 13 the Java String class got a new method named `stripIndent()` which can be used to strip out indentation, similarly to how indentation is stripped out of [Java Text Blocks](http://tutorials.jenkov.com/java/strings.html#java-text-blocks). The `stripIndent()` method is a preview feature, so we don't know if it will stay in Java yet. Here is an example of using the new Java String `stripIndent()` method:

```
String input  = "   Hey \n   This \n   is \n   indented.";
String output = input1.stripIndent();

System.out.println(output);

// output 
Hey
This
is
indented.
```
