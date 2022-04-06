# Loops

### For Loops

1. Loop initializer: It is optional. It can be initialized outside the loop
2. Loop condition
3. Post iteration operation: The post iteration statement is optional

```
for(int i=0; i < 10; i++) {
   System.out.println("i is: " + i);
}
```

{% hint style="info" %}
Curly braces are optional for single statement loops

```
for(int i = 0; i < 10; i++)
    System.out.println("i is 1: " + i);  // executed inside  loop.
    System.out.println("second line");   // executed after   loop.
```
{% endhint %}

{% hint style="info" %}
Multiple varriables can be initialized at the same time

```
for(int i=0, n=10; i < n; i++) {
}
```
{% endhint %}

### Continue

When the `continue` command is met, the Java Virtual Machine jumps to the next iteration of the loop without executing more of the `for` loop body

### Break

When the `break` command is met, the Java Virtual Machine breaks out of the `for` loop, even if the loop condition is still true.

### While Loop



```
int counter = 0;

while(counter < 10) {
    System.out.println("counter: " + counter);
    counter++;
}
```

### Do While Loop



```
InputStream inputStream  =  new FileInputStream("data/text.xml");

int data;
do {
    data = inputStream.read();
} while(data != -1);
```
