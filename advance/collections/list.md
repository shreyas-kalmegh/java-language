# List

The _Java List_ interface, `java.util.List`, represents an ordered sequence of objects. The elements contained in a Java `List` can be inserted, accessed, iterated and removed according to the order in which they appear internally in the Java `List`

### List vs. Set

that the same element can occur more than once in a Java `List`. This is different from a Java `Set` where each element can occur only once.

that the elements in a `List` has an order, and the elements can be iterated in that order. A Java `Set` does not make any promises about the order of the elements kept internally

### List Implementations



Since `List` is an interface you need to instantiate a concrete implementation of the interface in order to use it. You can choose between the following `List` implementations in the Java Collections API:

* java.util.ArrayList
* java.util.LinkedList
* java.util.Vector
* java.util.Stack
