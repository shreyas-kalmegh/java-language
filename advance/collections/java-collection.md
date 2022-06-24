# Java Collection



The following interfaces (collection types) extends the _Java_ _Collection_ interface:

* [List](https://jenkov.com/tutorials/java-collections/list.html)
* [Set](https://jenkov.com/tutorials/java-collections/set.html)
* [SortedSet](https://jenkov.com/tutorials/java-collections/sortedset.html)
* [NavigableSet](https://jenkov.com/tutorials/java-collections/navigableset.html)
* [Queue](https://jenkov.com/tutorials/java-collections/queue.html)
* [Deque](https://jenkov.com/tutorials/java-collections/deque.html)

Regardless of what Collection subtype you are using there are a few standard methods to add elements to a Collection

### Remove Element From Collection

```java
boolean wasElementRemoved = collection.remove("an element");
```

### Add Collection of Objects to Collection

```java
Set  aSet  = ... // get Set  with elements from somewhere

Collection collection = new HashSet();

collection.addAll(aSet);    //returns boolean too, but ignored here
```

### Remove Collection of Elements From Collection

```java
Collection objects = //... get a collection of objects from somewhere.

collection.removeAll(objects);
```

### Retain All Elements From a Collection in Another Collection



```java
Collection colA = new ArrayList();
Collection colB = new ArrayList();

colA.add("A");
colA.add("B");
colA.add("C");

colB.add("1");
colB.add("2");
colB.add("3");

Collection target = new HashSet();

target.addAll(colA);     //target now contains [A,B,C]
target.addAll(colB);     //target now contains [A,B,C,1,2,3]

target.retainAll(colB);  //target now contains [1,2,3]
```

### Checking if a Collection Contains a Certain Element



```java
Collection collection   = new HashSet();
boolean containsElement = collection.contains("an element");

Collection elements     = new HashSet();
boolean containsAll     = collection.containsAll(elements);
```

### Collection Size

```java
int numberOfElements = collection.size(); 
```
