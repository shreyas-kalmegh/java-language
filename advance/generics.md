# Generics

### **The Need for Generics**

```java
List list = new LinkedList();
list.add(new Integer(1)); 
Integer i = list.iterator().next(); // compile error
// Object returned by iterator needs to be casted

Integer i = (Integer) list.iterator.next();
```

```java
List<Integer> list = new LinkedList<>();
```

By adding the diamond operator <> containing the type, we narrow the specialization of this list to only _Integer_ type**\\**

We write generic methods with a single method declaration, and we can call them with arguments of different types. The compiler will ensure the correctness of whichever type we use.
