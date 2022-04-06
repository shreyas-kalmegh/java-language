# Packages

A Java package is like a directory in a file system. In fact, on the disk a package is a directory. All Java source and class files of classes belonging to the same package are located in the same directory.

![Java Package example](<../.gitbook/assets/image (1).png>)

Package list in above example:

* com
* collections
* concurrency
* concurrent
* date

Subpackages list in above example

* jenkov
* navigation

{% hint style="info" %}
src is source root and not a package. All the directories below it are packages/subpackages
{% endhint %}

Example of adding a class to a package

```
package com.jenkov.navigation;

public class Page {
    ...
}
```

### Importing A Class

```
com.jenkov.navigation.Page
```

### Naming Conventions

To avoid creating packages with the same names as other public Java packages it is recommended that you start your package hierarchy with the reverse domain name of your company. For instance, since the domain name of my company is `jenkov.com` I should start with a package structure called `com.jenkov`.

### How to Divide Your Classes Into Packages

* **Divide by Layer:** For instance, your application may have a database layer. Then you would create a database package. All classes involved in communication with the database would then be located in the database package.
* **Divide by Application Functionality:** The second method is to divide your classes based on what part of the application functionality they belong to. Thus, if your application has a functionality area which calculates pensions, you might create a Java package named `pension`
