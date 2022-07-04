# Java Map

The _Java Map_ interface, `java.util.Map`, represents a mapping between a key and a value. More specifically, a _Java_ _Map_ can store pairs of keys and values



Since `Map` is an interface you need to instantiate a concrete implementation of the `Map` interface in order to use it. The Java Collections API contains the following `Map` implementations:

* java.util.HashMap: `HashMap` maps a key and a value. It does not guarantee any order of the elements stored internally in the map.
* java.util.Hashtable
* java.util.EnumMap
* java.util.IdentityHashMap
* java.util.LinkedHashMap
* java.util.Properties
* java.util.TreeMap: `TreeMap` also maps a key and a value. Furthermore it guarantees the order in which keys or values are iterated - which is the sort order of the keys or values. Check out the Java `Map` JavaDoc for more details.
* java.util.WeakHashMap

{% hint style="info" %}
The HashMap implementation is typically the fastest of the two Map implementations, so whenever you don't need to sort the elements in the Map you can just use a HashMap. Otherwise use a TreeMap.
{% endhint %}

### Create a Map



```java
Map mapA = new HashMap();
Map mapB = new TreeMap();

// Generic implementation
Map<String, MyObject> map =
    new HashMap<String, MyObject>();
```

### Inserting Elements Into a Java Map

```java
Map<String, String> map = new HashMap<>();

map.put("key1", "element 1");
```

{% hint style="info" %}
Only Java objects can be used as keys and values in a Java Map. In case you pass primitive values (e.g. int, double etc.) to a `Map` as key or value, the primitive values will be auto-boxed before being passed as parameters
{% endhint %}

### Null Keys



Quite surprisingly you can use the value `null` as a key in a Java Map. Here is an example of using a `null` key in a Java Map:

```java
Map map = new HashMap();

map.put(null, "value for null key");
```

### Inserting All Elements From Another Map



```
Map<String, String> mapB = new HashMap<>();
mapB.putAll(mapA);
```

### Get or Default Value

The Java `Map` interface has a `getOrDefault()` method which can return a default value supplied by you - in case no value is stored in the `Map` by the given key.



```
String value = map.getOrDefault("E", "default value")
```

### Checking if Map Contains Key



```
boolean hasKey = map.containsKey("123");
boolean hasValue = map.containsValue("value 1");
```

### Iterating the Keys of a Java Map



```
Map<String, String> map = new HashMap<>();

Iterator<String> iterator = map.keySet().iterator();

while(iterator.hasNext(){
  String key   = iterator.next();
  String value = map.get(key);
}

// OR
for(String key : map.keySet()) {
    String value = map.get(key);
}

// OR
Stream<String> stream = map.keySet().stream();
stream.forEach((value) -> {
    System.out.println(value);
}); 
```

{% hint style="info" %}
Similarly, we can iterate over values using map.values() instead of map.keys()
{% endhint %}

### Iterating the Entries(Key, Value) of a Java Map



```java
Set<Map.Entry<String, String>> entries = map.entrySet();

Iterator<Map.Entry<String, String>> iterator =
    entries.iterator();

while(iterator.hasNext()) {
    Map.Entry<String, String> entry = iterator.next();
    String key   = entry.getKey();
    String value = entry.getValue();
}

// OR
for(Map.Entry<String, String> entry : map.entrySet()){
    String key = entry.getKey();
    String value = entry.getValue();
}
```

### Removing Entries From a Java Map

```
map.remove("key1");
```

### Removing All Entries

```
map.clear();
```

### Replacing an Entry in a Java Map

The `replace()` method will only insert the new value if there is already an existing value mapped to the key. If no existing value is mapped to the given key, no value is inserted. This is different from how `put()` works, which always insert the value no matter what.



```
map.replace("key", "val2"); //no "key" entry, no replace

map.put("key", "val1");     //now contains "key" entry

map.replace("key", "val2"); //now "key" entry replaced
```

### Functional Operations in Java Map



The functional operation methods are:

* compute()
* computeIfAbsent()
* computeIfPresent()
* merge()

#### compute()

The `Map` `compute()` method takes a key object and a lambda expression as parameters. The lambda expression must implement the `java.util.function.BiFunction` interface

Whatever value the lambda expression returns is stored instead of the currently stored value for that key. If the lambda expression returns `null`, the entry is removed. There will not be a key -> `null` mapping stored in the `Map`.

```
map.compute("123", (key, value) ->     
value == null ? null :       
  value.toString().toUpperCase());
```

#### computeIfAbsent()

The `Map` `computeIfAbsent()` method works similarly to the `compute()` method, but the lambda expression is only called if no entry exists already for the given key

The value returned by the lambda expression is inserted into the `Map`. If `null` is returned, no entry is inserted.

```
map.computeIfAbsent("123", (key) -> "abc");
```

#### computeIfPresent()

The `Map` `computeIfPresent()` method works oppositely of `computeIfAbsent()`. It only calls the lambda expression passed as parameter to it, if an entry already exists in the `Map` for that key.

```
map.computeIfPresent("123", (key, value) -> 
    value == null ? null :       
      value.toString().toUpperCase());
```

#### merge

If the `Map` does not have an entry for the key, or if the value for the key is null, the value passed as parameter to the `merge()` method is inserted for the given key.

If, however, an existing value is already mapped to the given key, the lambda expression passed as parameter is called instead. The lambda expression thus gets a chance to _merge_ the existing value with a new value. The value returned by the lambda expression is then inserted into the `Map` for the given key. If the lambda expression returns `null`, the entry for the given key is removed.



```
map.merge("123", "XYZ",     (oldValue, newValue) -> newValue + "-abc");
```
