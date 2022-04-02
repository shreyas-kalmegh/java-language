# How JAVA Program Works

![](https://docs.oracle.com/javase/tutorial/figures/getStarted/getStarted-compiler.gif)

1. all source code is first written in plain text files ending with the `.java` extension
2. Those source files are then compiled into `.class` files by the `javac` compiler
3. A `.class` file does not contain code that is native to your processor; it instead contains _bytecodes_ — the machine language of the Java Virtual Machine[1](https://docs.oracle.com/javase/tutorial/getStarted/intro/definition.html#FOOT) (Java VM). The `java` launcher tool then runs your application with an instance of the Java Virtual Machine.

![The API and Java Virtual Machine insulate the program from the underlying hardware.](https://docs.oracle.com/javase/tutorial/figures/getStarted/getStarted-jvm.gif)
