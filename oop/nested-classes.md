# Nested Classes

The purpose of a nested class is to clearly group the nested class with its surrounding class, signaling that these two classes are to be used together. Or perhaps that the nested class is only to be used from inside its enclosing (owning) class.



You can create several different types of nested classes in Java. The different Java nested class types are:

* Static nested classes
* Non-static nested classes
* Local classes
* Anonymous classes

### Static Nested Classes



```
public class Outer {
  public static class Nested {
  }
}
Outer.Nested instance = new Outer.Nested();
```

### Non-static Nested Classes (Inner Classes)



```
public class Outer {
  public class Inner {
  }
}
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();
```

{% hint style="info" %}
Non-static nested classes (inner classes) have access to the fields of the enclosing class, even if they are declared private
{% endhint %}

### Inner Class Shadowing

In the example both the `Outer` and `Inner` class contains a field named `text`. When the `Inner` class refers to `text` it refers to its own field. When `Outer` refers to `text` it also refers to its own field.

```
public class Outer {

    private String text = "I am Outer private!";

    public class Inner {
        private String text = "I am Inner private";
        public void printText() {
            System.out.println(text);
        }
    }
}
```

### Local Classes



Local classes in Java are like inner classes (non-static nested classes) that are defined inside a method or scope block (`{ ... }`) inside a method. Here is an example:

```
class Outer {

    public void printText() {
        class Local {
        }
        Local local = new Local();
    }
}
```

Local classes can only be accessed from inside the method or scope block in which they are defined.

Local classes can access members (fields and methods) of its enclosing class just like regular inner classes.

Local classes can also access local variables and parameters inside the same method or scope block, provided these variables are declared `final`

Local classes can also be declared inside static methods. In that case the local class only has access to the static parts of the enclosing class

### `Anonymous Class`

Anonymous classes in Java are nested classes without a class name. They are typically declared as either subclasses of an existing class, or as implementations of some [interface](https://jenkov.com/tutorials/java/interfaces.html).



```
public class SuperClass {

  public void doIt() {
    System.out.println("SuperClass doIt()");
  }
}
SuperClass instance = new SuperClass() {
  // this is an anonymous class extending SuperClass
    public void doIt() {
        System.out.println("Anonymous class doIt()");
    }
};
instance.doIt();
```

### Use Case

The benefits of Java nested classes are that you can group classes together that belong together

Example:&#x20;

```
public class Cache {

    private Map<String, CacheEntry> cacheMap = new HashMap<String, CacheEntry>();

    private class CacheEntry {
        public long   timeInserted = 0;
        public object value        = null;
    }

    public void store(String key, Object value){
        CacheEntry entry = new CacheEntry();
        entry.value = value;
        entry.timeInserted = System.currentTimeMillis();
        this.cacheMap.put(key, entry);
    }

    public Object get(String key) {
        CacheEntry entry = this.cacheMap.get(key);
        if(entry == null) return null;
        return entry.value;
    }

}
```
