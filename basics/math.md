# Math

### Operators

| Math Operator | Description             |
| ------------- | ----------------------- |
| `+`           | Performs addition       |
| `-`           | Performs subtraction    |
| `*`           | Performs multiplication |
| `/`           | Performs division       |
| +=            |                         |
| -=            |                         |
| \*=           |                         |
| /=            |                         |
| %=            |                         |

### Java Math Operator Precedence

he math operators `*` and `/` for multiplication and division takes precedence over the `+` and `-` operators. That means, that multiplications and divisions are evaluated before addition and subtraction in math expressions. In case there are **multiple `*` and `/` operators they will be calculated from left to right**

****

```
int result = 100 * 100 / 5 + 200 * 3 / 2;

100 * 100 = 10000;
10000 / 5 = 2000;

200 * 3 = 600;
600 / 2 = 300;

int result = 2000 + 300;
```

You can control the operator precedence and sequence of calculations in math expressions in Java using **parentheses**. Math expressions inside parentheses have higher precedence than any other operator. Therefore expressions inside parentheses are calculated **first**. Inside parentheses the normal operator precedence applies.

### Integer Math



```
int result = 100 / 8;

// result=12
```

### Java Floating Point Math

Java contains the two floating point data types `float` and `double`. These floating point types are capable of containing fractions in the numbers



```
double result = 100 / 8;
```

since the two values in the math expression (100 and 8) are both integers, result will be 12 and not 12.5

{% hint style="info" %}
To avoid rounding of calculations in math expressions in Java you must make sure that all data types involved in the math expression are floating point types.
{% endhint %}

Java has a way to force all numbers in a calculation to be floating point variables. You suffix the numbers with either a capital F or D. Here is an example:

```
double result = 100D / 8D;
```

{% hint style="warning" %}
Java floating point data types are not 100% precise. You can experience situations where numbers with many fractions on do not add up to the number you expected. If a floating point calculation results in a number with more fractions than a `float` or a `double` can handle, fractions may be cut of
{% endhint %}

### Math Class Functions

* Math.abs()
* Math.floor()
* Math.ceil()
* Math.floorDiv()
* Math.round()
* Math.random()

etc..
