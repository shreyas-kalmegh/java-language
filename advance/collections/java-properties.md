# Java Properties

The _Java_ _Properties_ class, `java.util.Properties`, is like a [Java Map](https://jenkov.com/tutorials/java-collections/map.html) of [Java String](https://jenkov.com/java/strings.html) key and value pairs. The Java `Properties` class can write the key, value pairs to a _properties_ file on disk, and read the _properties_ back in again. This is an often used mechanism for storing simple configuration _properties_ for Java applications.



### Create a Properties Instance

To use the Java `Properties` class you must first create a `Properties` instance. You do so via its constructor and the Java `new` instruction. Here is an example of creating a Java `Properties` instance:

```java
Properties properties = new Properties();
```

### Get/Set/Remove/Iterate



```java
properties.setProperty("email", "john@doe.com");
String email = properties.getProperty("email");
properties.remove("email");


Iterator keyIterator = properties.keySet().iterator();

while(keyIterator.hasNext()){
    String key   = (String) keyIterator.next();
    String value = properties.getProperty(key);
    System.out.println(key + " = " + value );
}
```



### Store Properties to File

You can store the property key, value pairs to a properties file which can be read again later on. You store the contents of a `Properties` object via its `store()` method. Here is an example of storing the contents of a Java `Properties` to a properties file:

```java
Properties properties = new Properties();

properties.setProperty("property1", "value1");
properties.setProperty("property2", "value2");
properties.setProperty("property3", "value3");

try(FileWriter output = new FileWriter("data/props.properties")){
    properties.store(output, "These are properties");
} catch (IOException e) {
    e.printStackTrace();
}
```



### Load Properties From File

You can also load properties stored in a property file back into a Java `Properties` object via its `load()` method. Here is an example of loading a property file into a Java `Properties` object:

```java
Properties properties = new Properties();

try(FileReader fileReader = new FileReader("data/props.properties")){
    properties.load(fileReader);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Property File Format

A Java `Properties` property file consists of lines with one `key=value` pair on each line. Here is an example Java `Properties` property file:

```java
#These are properties
#Thu Jul 04 21:29:20 CEST 2019
property2=value2
property1=value1
property3=value3
```



#### Default Values With getProperty()

The `getProperty()` method comes in a version that takes an extra parameter which is the default value to return in case the `Properties` instance does not contain a value for the given key. Here is an example of calling `getProperty()` with a default value:

```java
Properties properties = new Properties();

String preferredLanguage =
    properties.getProperty("preferredLanguage", "Danish");
```

### Properties is a Subclass of Hashtable - by Mistake!

The Java `Properties` class is a subclass of the Java `Hashtable` class, and as I will show you - this is actually a design mistake! It is a great example of when the classic "Is a / Has a" OOP rule about when to use inheritance vs. composition fails. Let's see how.

Being a subclass of `Hashtable`, you can actually use the `get()` and `put()` method of the `Hashtable` class, which allow the use of non-string keys and values. This defeats the purpose of the `Properties` class, which is to function as a string,string map. Here is an example of using `put()` on `Properties`:

```java
Properties asProperties = new Properties();

asProperties.put(123, 456);
asProperties.put("abc", 999);
```

Notice how it is possible to call `put()` with non-string values.Just to make it clear: You should NOT use the `put()` and `get()` method of the `Properties` class!
