# Access Modifiers





* private: The `private` access modifier means that only code inside the class itself can access this Java field.
* package: The `package` access modifier means that only code inside the class itself, or other classes in the same package, can access the field. This is the default access modifier
* protected: The `protected` access modifier is like the `package` modifier, except subclasses of the class can also access the field, even if the subclass is not located in the same package.
* public: The `public` access modifier means that the field can be accessed by all classes in your application.



|              | private | default | protected | public |
| ------------ | ------- | ------- | --------- | ------ |
| Class        | No      | Yes     | No        | Yes    |
| Nested Class | Yes     | Yes     | Yes       | Yes    |
| Constructor  | Yes     | Yes     | Yes       | Yes    |
| Method       | Yes     | Yes     | Yes       | Yes    |
| Field        | Yes     | Yes     | Yes       | Yes    |

### Class Access Modifiers

It is important to keep in mind that the Java access modifier assigned to a Java class takes precedence over any access modifiers assigned to fields, constructors and methods of that class. If the class is marked with the `default` access modifier, then no other class outside the same Java package can access that class, including its constructors, fields and methods. It doesn't help that you declare these fields `public`, or even `public static`.
