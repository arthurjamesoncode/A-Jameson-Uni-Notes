### Declaring Variables
When we code in Java, we need to **declare** variables. We do this so that we can represent some data of some specific data type with a meaningful name. This allows us to create code that can act on many different values, or to track some changing value throughout your code.

We can see some example declarations below:
```java
double currentWeight;
int studentsLearningJava;
int maximumValue;

studentsLearningJava = 78;
maximumValue = 120;
maximumValue = studentsLearningJava;
```

As you can see, when you declare a variable in Java, you must start with the type of the variable, for example `int` or `double`, followed by an identifier. Java will then set aside the required memory to store some data of this type. So the first declaration sets enough space aside for a `double` and the next two set aside enough for an `int` each.

Identifier's must be **legal identifiers** which means they must start with one of:
- A letter,
- An underscore,
- A dollar sign,
And they can only contain:
- Letters,
- Digits,
- Underscores,
- Dollar signs

It's worth noting that, by **convention**, variables should be named in camel case starting with a lower case letter.

While you do not need to follow convention, it helps code look consistent. This helps more than you think when it comes to reading and debugging code.

Not that we don't actually need to give a value (called initialising) when we declare the variable, we can initialise our variables later. You can see this in the first 3 lines. However if we try to use an **uninitialized** variable, we might will get an error
```
error: variable test might not have been initialized
```
where `test` is the name of the uninitialized variable.

>We only get an error if `test` is a **local** variable. This will be discussed in more detail in [[Lecture 4 - Intro to Java Control Flow]]. 

As you can see from the second block of declarations, we can assign values to uninitialized variables as well as reassign values to already initialised variables.

The key things to understand is that defining a variable's name and type is called a **declaration** and uses the syntax
```java
type variableName;
```
while assigning a value to a variable is called **assignment** and uses the syntax.
```java
variableName = <value>;
```

When we assign the first value to a variable we call it **initialisation**. Initialisation can be done in the same line as the declaration but doesn't have to be.

For example:
```java
int num = 1;

//OR

int number;
number = 1;
```
## Strongly Typed Languages
Java is an example of a strongly typed language. This means it is a language that enforces us to declare the **type** of our variables, and that the types of our variables won't be automatically changed at run time.

This has a few big advantages:
- Prevents accidental (or malicious) memory access
- Captures preventable runtime errors at compile time
- Limits unexpected behaviour caused by automatic type conversions
- Improves code readability, and therefore maintainability, by telling developers what every variable is

For example:
```java
int x = 1;
String y = " two " ;

x = y ; // compiler complains , not your users !
```
## Primitive Types
In java there are several primitive data types. These are the only things in Java not considered objects and represent raw values. These primitive data types all take up a different amount of space and can hold a different range of values.

Four of the primitive data types can hold **integer** values:
- **byte** - Size 1 Byte - Range -128 to 127
- **short** - Size 2 Bytes - Range -32,768 to 32,767
- **int** - Size 4 Bytes - Range -2,147,483,648 to 2,147,483,647
- **long** - Size 8 Bytes - Range $\pm9.22e18$ 

Two of the primitive data types can hold **floating point** values:
- **float** - Size 4 Bytes - Precision 6-7 digits
- **double** - Size 8 Bytes - Precision 15-16 digits

>For more info on floating point representations in binary you can look to [[Lecture 27 - Adder Circuits and Two's Complement]]

We also have two primitive data types for storing non-numeric values:
- **char** - Size 2 Bytes - Represents a single Unicode character
- **boolean** - Size 1 Bit - Has a value of either 1 or 0 

>Note that the actual stored size of a boolean value, despite only needing 1 bit, depends on the virtual machine that runs it. It is very unlikely that you will need to understand this in detail, as it shouldn't affect how you implement most code.

It is also worth talking about **strings**, which are a primitive data type in many languages and are still widely used in Java. Strings in Java are actually not a primitive data type, instead they are a class, with associated methods that allow us to interact with them. You can see that they are a class and not a primitive data type as when `String` variables are declared they are declared with 
```java
String name = "value"
```
Instead of 
```java
string name = "value"
```

We will discuss strings more later in the course, but all you need to know for now is that, when defining strings, you must use double quotes and not single quotes, as single quotes are are only used for **char** values.

For example:
```java
//VALID
String name = "Test String!"
String x = "X"
char a = 'A'

//INVALID
String name = 'Test String!'
String x = 'x'
char a = "A"
```
## Type Casting
Sometimes, we will want to convert variables between compatible primitive data types. This is called type casting. This can go two ways, we either **widen** the value, or we **narrow** the value.

**Widening Casting**, which can be done automatically, is when we cast a variable of a **smaller** type to a **larger** type. There are 19 specific conversions which we call widening primitive conversions:
- `byte to short, int, long, float, or double`
- `short to int, long, float, or double`
- `char to int, long, float, or double`
- `int to long, float, or double`
- `long to float or double`
- `float to double`

A widening conversion will never lose information about the overall magnitude of a numeric value.

>Note that, as `char` is actually just a number under the hood that it can be cast into the numeric types. Smaller types can not be cast into `char` as `char` can only hold positive values and therefore does not hold a wider range than types like `byte` or `short`.

An example of widening casting is:
```java
int myInt = 9;
double myDouble = myInt; // Automatic casting: int to double

System.out.println(myInt);    // Outputs 9
System.out.println(myDouble); // Outputs 9.0
```

**Narrowing Casting**, which has to be done manually, is when we cast a variable of a **larger** type to a **smaller** type. There are 22 specific conversions which we call narrowing primitive conversions:
- `short to byte or char`
- `char to byte or short`
- `int to byte, short, or char`
- `long to byte, short, char, or int`
- `float to byte, short, char, int, or long`
- `double to byte, short, char, int, long, or float`

A narrowing conversion may lose information about the magnitude of a numeric value, and could also lose precision.

We can cast a variable of a larger type, say `double`, to a smaller type, say `int`, by surrounding the smaller type in brackets before the larger value. This tells java that we must change the type of the variable to the type in brackets.

An example of narrowing casting is:
```java
double myDouble = 9.78d;
int myInt = (int) myDouble; // Manual casting: double to int

System.out.println(myDouble); // Outputs 9.78
System.out.println(myInt);    // Outputs 9
```
## Constants
Constants are defined and named values, which don't change over the runtime of the program.

They can be declared using the following syntax
```java
final <type> <CONSTANT_NAME> = <value>;
```
- `final` is a keyword which denotes that what follows is a constant declaration
- `<type>` and `<value>` can be any pair of compatible primitive type and value.
- `<CONSTANT_NAME>` must be a legal identifier. By convention, identifiers for constants should be written in all caps, with words separated by underscores.

We use constants for 3 main reasons:
- **Efficiency:** Compiler optimizations will result in smaller binary code and memory footprint if constants are used.
- **Readability:** Allows *magic numbers* to be replaced by labels, making it easier to understand what code is doing.
- **Ease of Maintenance:** Imagine if you had written a financial program which included VAT calculations. If you didn't store VAT as a constant and instead wrote `0.2` whenever you needed to do VAT calculations. If VAT changed one year to 25%, you would need to change your code in order to include `0.25` where ever `0.2` was before. If, instead, you had a constant called `VAT` with a value of `0.2` you would then only need to change that one value.

To see an example of how constants improve readability, compare the two programs below.
```
result = ASSIGNMENT_WEIGHT * assignment
	   + LABS_WEIGHT * lab
	   + EXAM_WEIGHT * exam;
```
VS
```
result = 0.75 * assignment + 0.10 * lab + 0.15 * exam ;
```
As you can see it's far clearer what the first program is doing, compared to the second one.